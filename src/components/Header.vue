<template>
	<header class="header">
		<div class="header__container container">
			<h1 class="header__logo">
				<a href="">Twitter</a>
			</h1>
		<nav class="nav">
			<ul class="nav__list">
				<li class="nav__item">
					<a class="nav__link">
						Bem vindo(a): <br />
						<strong>{{ user }}</strong>
					</a>
				</li>
				<li class="nav__item">
					<a class="nav__link" href="/">Página Inicial</a>
				</li>
				<li class="nav__item">
					<a class="nav__link">Hashtags</a>
				</li>
				<li class="nav__item">
					<a class="nav__link">Logout</a>
				</li>
			</ul>
		</nav>
		</div>
	</header>
</template>

<script>
export default {
	name: 'Header',
	props: {
  	user: {
			type: String,
			required: true,
			default: ""
		}
	},
  data () {
    return {
      
    }
  }
}
</script>

<style scoped>
	.header {
		width: 100%;
		background-color: #fff;
	}

	.header__container {
		padding: 0 15px;
		display: flex;
		text-align: center;
		justify-content: space-between;
		align-items: center;
		flex-wrap: wrap;
	}
	/* @media (max-width: 610px) {
		.header__container {
			justify-content: center;
		}
	} */
	.header__logo {
		padding: 13px 0px;
	}

	.header__logo a {
		color: inherit;
		text-decoration: none;
	}

	.header__item {
		display: inline-block;
	}

	/* @media (max-width: 610px) {
		.nav__list {
			text-align: center;
		}
	} */
	.nav__item {
		display: inline-block;
		vertical-align: middle;
	}
	.nav__link {
		padding: 14px 10px;
		display: block;
		cursor: pointer;
	}
	/* @media (max-width: 610px) {
		.nav__link {
			padding: 14px 7px;
			font-size: 11px;
		}
	} */
	
</style>
