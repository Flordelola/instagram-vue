<template>
  <div>
    <the-header
      :step="step"
      @go-to="handleGoTo"
      @next-step="step++"
      @share-post="handleShare"
    />
    <the-container 
      :step="step"
      :posts="posts"
      :filters="filters"
      :image="image"
      v-model="caption"
      @filter-selected="handleFilterSelected"
    />
    <the-footer
      :step="step"
      @go-to="handleGoTo"
      @upload-image="handleUploadImage"/>

  </div>
</template>

<script>
  import posts from '@/data/posts'
  import filters from '@/data/filters'
  import TheHeader from '@/components/TheHeader.vue'
  import TheContainer from '@/components/TheContainer.vue'
  import TheFooter from '@/components/TheFooter.vue'

  export default {
    name: 'Home',
    data () {
      return {
        posts,
        filters,
        caption: '',
        image: '',
        step: 1
      }
    },
    components: {
      TheHeader,
      TheContainer,
      TheFooter
    },
    methods: {
      handleGoTo () {
        this.caption = ''
        this.image = ''
        this.step = 1
      },
      handleShare () {
        const post = {
        username: 'FlordeLola',
        userImage: 'data:image/jpeg;base64,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',
          postImage: this.image,
          likes: 0,
          caption: this.caption,
          filter: this.filterType
        }
        this.posts.unshift(post)
        this.handleGoTo()
      },
      handleUploadImage (ev) {
        const files = ev.target.files
        if (!files.length) return

        const reader = new FileReader()
        reader.readAsDataURL(files[0])
        reader.onload = ev => {
          this.image = ev.target.result
          this.step = 2
        }
        document.querySelector('#file').value = ''
      },
      handleFilterSelected (ev) {
        this.filterType = ev.filter
      } 
    }
  }
</script>
