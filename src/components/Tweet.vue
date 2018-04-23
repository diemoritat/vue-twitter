<template>
  <article class="tweet">
		<div class="tweet__header">
			<img 
				class="tweet__avatar" 
				:src="tweetInfo.usuario.foto" 
				:alt="userName"
			/>
			<span class="tweet__name">{{ userName }}</span>
		</div>

		<p class="tweet__content">{{ content }}</p>

		<footer class="tweet__footer">
			<button class="btn btn--clean">
				<svg class="icon icon--small iconHeart" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 47.5 47.5">
					<defs>
						<clipPath id="a">
							<path d="M0 38h38V0H0v38z"></path>
						</clipPath>
					</defs>
					<g clipPath="url(#a)" transform="matrix(1.25 0 0 -1.25 0 47.5)">
						<path d="M36.885 25.166c0 5.45-4.418 9.868-9.867 9.868-3.308 0-6.227-1.632-8.018-4.128-1.79 2.496-4.71 4.129-8.017 4.129-5.45 0-9.868-4.418-9.868-9.868 0-.773.098-1.52.266-2.242C2.75 14.413 12.216 5.431 19 2.965c6.783 2.466 16.249 11.448 17.617 19.96.17.721.268 1.47.268 2.241"></path>
					</g>
				</svg>
				0
			</button>
		</footer>
	</article>
</template>

<script>
export default {
	name: 'Tweet',
	props: {
		tweetInfo: {
			type: Object,
			required: true
		},
		content: {
			type: String,
			required: true
		}
	},
	data() {
		return {

		}
	},
	computed: {
		userName() {
			return `${ this.tweetInfo.usuario.nome} ${ this.tweetInfo.usuario.sobrenome}`;
		}
	}
}
</script>

<style scoped>
	/* tweet */
	.tweet {
		position: relative;
		padding-left: 75px;
		padding-right: 15px;
		width: calc(100% - 90px);
		margin-left: -15px;
		text-align: left;
	}
	.tweet:not(:last-child) {
		border-bottom: 2px solid #e6ecf0;
		padding-bottom: 15px;
		margin-bottom: 15px;  
	}
	.tweet__name {
		font-size: 14px;
		font-weight: bold;
		margin-right: 4px;
	}
	.tweet__userName {
		font-size: 14px;
	}
	.tweet__avatar {
		position: absolute;
		top: 0;
		left: 15px;
		width: 45px;
		height: 45px;
	}
	.tweet__content {
		font-size: 14px;
		line-height: 20px;
		white-space: pre-wrap;
		word-wrap: break-word;
		text-align: left;
	}
	.tweet__footer {
		margin-top: 10px;
	}
</style>
