<template>
  <div class="link-list">
    <div class="list-item">
      <h1>{{ $t('PODCATCHER') }}</h1>
      <ul>
        <li v-for="(entry, index) in data" :key="index">
          <a
            :href="constructURL(entry)"
            target="_blank"
            @click="onClick(entry, constructURL(entry))"
          >
            <icon v-if="entry.icon" :type="entry.icon"></icon>
            <span class="link-title">{{ entry.title }}</span>
            <icon type="arrow-to-right"></icon>
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { selectFeed } from 'store/selectors'
import { Icon } from '@podlove/components'
import { getPlatform } from '@podlove/utils/useragent'

export default {
  components: { Icon },
  props: {
    data: {
      type: Array,
      default: null
    }
  },
  data() {
    return {
      ...this.mapState({
        feed: selectFeed
      }),
      platform: getPlatform()
    }
  },
  methods: {
    constructURL(item) {
      const regex = /^https:\/\//gm
      let url = ''
      if (item.https) {
        url = this.feed[0].url
      } else {
        url = this.feed[0].url.replace(regex, '')
      }

      if (item.platform[this.platform]) {
        return `${item.platform[this.platform].scheme}${url}`
      } else if (item.platform['web']) {
        return `${item.platform['web'].scheme}${url}`
      }
    },
    onClick(client, composedUrl) {
      this.$emit('click', client, composedUrl)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~theme/variable';
h1 {
  border-bottom: 1px dotted #626262;
}
.link-list {
  width: 100%;
  padding: 0 2em;
  overflow-y: auto;
  max-height: calc(100vh - #{$upper-content-height} - #{$footer-content-height} - 10px);
}

.list-item {
  ul {
    list-style: none;
    padding-left: 0px;

    li {
      padding: 0.75em 0;
      cursor: pointer;

      &:hover {
        background: rgba($color: #000, $alpha: 0.3);
      }

      a {
        display: flex;
        align-items: center;

        .link-title {
          margin: 0 0.5em 0 1em;
        }
      }
    }
  }
}
</style>
