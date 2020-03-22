
<template>
  <article class="card-post">
    <div class="header level">
      <div class="level-left">
        <figure class="image is-32x32">
          <img :src="post.userImage" :alt="post.username" />
        </figure>
        <span class="username">{{post.username}}</span>
      </div>
    </div>
    <div class="image-container"
      :class="post.filter"
      :style="{ backgroundImage: 'url(' + post.postImage + ')' }"
      @dblclick="like">
    </div>
    <div class="content">
      <div class="heart">
          <button @click="like" aria-label="You like">
            <i class="far fa-heart fa-lg" :class="{'fas': this.post.hasBeenLiked}"></i>
          </button>
      </div>
      <p class="likes">{{post.likes}} likes</p>
      <p class="caption"><span>{{post.username}}</span> {{post.caption}}</p>
    </div>
  </article>
</template>

<script>
export default {
  name: 'cardPost',
  props: {
    post: Object
  },
  methods: {
    like () {
      this.post.hasBeenLiked ? this.post.likes-- : this.post.likes++
      this.post.hasBeenLiked = !this.post.hasBeenLiked
    }
  }
}
</script>

<style lang="css">

	.card-post {
		margin: 0 auto;
		width: 500px;
		height: 500px;
		border: 1px solid #cccccc;
		margin-bottom: 15px;
	}

	.card-post .header {
		height: 30px;
		border-bottom: 1px solid #fff;
		margin: 7.5px 10px;
	}
	.card-post .header .level-left {
		display: flex;
		flex-direction: row;
		align-items: center;
	}

	.card-post .header .image {
		display: inline-block;
		margin: 0;
	}

	.card-post .header figure, img {
		border-radius: 100%;
		height: 32px;
		width: 32px;
	}

	.card-post .header .username {
		position: relative;
		padding-left: 5px;
		font-size: 0.9rem;
		font-weight: bold;
	}
	.card-post .level {
		margin-bottom: 0.5rem !important;
	}

	.card-post .image-container {
		height: 330px;
		background-repeat: no-repeat;
		background-position: center center;
		background-size: cover;
	}

	.card-post .content {
		margin: 7.5px 10px;
	}

	.card-post .heart button {
		border: 0 solid;
		padding: 0;
		background: none;
	}

	.card-post .far.fa-heart,
	.fas.fa-heart {
		cursor: pointer;
	}

	.card-post .fas.fa-heart {
		color: #f06595;
	}

	.card-post .likes {
		margin: 5px 0;
		margin-bottom: 5px !important;
		font-size: 0.85rem;
		font-weight: bold;
	}

	.caption {
		font-size: 0.85rem;
	}
	.caption span  {
		font-weight: bold;
	}
	.card-post aption span {
		font-weight: bold;
	}
	.card-post:last-child {
		margin-bottom: 50px;
	}
</style>