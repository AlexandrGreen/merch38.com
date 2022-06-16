<template>
	<q-page class="constructor">
		<div class="constructor__container">

			<div class="constructor__header">
				<div class="constructor-header">
					<span class="constructor-header__title">Upload your image and preview your pretty cup!</span>
					<div
						@click="pick_files()"
						class="constructor-header__button button-typical button-typical_color_yellow"
					>Upload</div>
				</div>
			</div>

			<div class="constructor__body">
				<q-uploader
					ref="uploader"
					:max-files="1"
					class="constructor__uploader uploader"
				>
					<template v-slot:header="scope">
						<q-uploader-add-trigger/>
					</template>
					<template v-slot:list="scope">

						<div class="draggable uploader__draggable draggable_type_cup">
							<div class="draggable__area">
								<div
									v-for="file in scope.files"
									:key="file.__key"
									class="draggable__image-wrap"
								>
									<img
										v-if="file.__img"
										:src="file.__img.src"
										alt=""
										class="draggable__image"
									>
								</div>
							</div>
						</div>

					</template>
				</q-uploader>
			</div>

		</div>
	</q-page>
</template>

<script>
import {defineComponent, ref} from 'vue'
import domtoimage from 'dom-to-image'

export default defineComponent({
	name: 'IndexPage',

	setup() {
		const uploaded = ref([]),
			uploader = ref(null),
			pick_files = () => {
				uploader.value.removeQueuedFiles();
				uploader.value.pickFiles();
			},
			save = () => {
			alert(123)
			};

		return {
			uploaded,
			uploader,
			pick_files,
			save,
		}
	},
})
</script>

<style lang="scss" scoped>
$color_yellow: #fec93f;

.constructor {
	padding: 20px;
	display: flex;
	align-items: center;
	justify-content: center;

	&__container {
		max-width: 50vw;
		border-radius: 30px;
		border: 1px solid #1D1D1D;
	}

	&__header, &__body {
		padding: 20px;
	}

	&__header {
		display: flex;
		align-items: center;
		border-bottom: 1px solid #1D1D1D;
	}

	&__uploader {
		width: 100%;
	}
}

.constructor-header {
	display: flex;
	flex-wrap: wrap;
	align-items: center;
	margin: -15px 0 0 -20px;
	justify-content: center;

	& > * {
		margin: 15px 0 0 20px;
	}

	&__title {
		font-size: 20px;
		text-align: center;
		border-bottom: 2px solid $color_yellow;
	}

	&__button {

	}
}

.button-typical {
	height: 40px;
	display: flex;
	padding: 0 30px;
	font-size: 13px;
	cursor: pointer;
	font-weight: 700;
	align-items: center;
	white-space: nowrap;
	border-radius: 100px;
	text-decoration: none;
	justify-content: center;
	text-transform: uppercase;

	&_color_yellow {
		color: #000;
		background-color: $color_yellow;
	}

	&_color_brown {
		color: #fff;
		background-color: #B88845;
	}

	&_color_gray {
		color: #fff;
		background-color: #686868;
	}
}

.uploader {
	width: 100%;
	display: flex;
	box-shadow: none;
	border-radius: 0;
	max-height: unset;
	align-items: center;
	flex-direction: column;

	:deep(.q-uploader__list) {
		width: 60%;
		padding: 0;
		display: flex;
		min-height: unset;
		align-items: center;
		justify-content: center;
		background-size: contain;
		background-position: center;
		background-repeat: no-repeat;
		background-image: url(../../public/images/objects/object.webp);
	}

	:deep(.q-uploader__list:after) {
		content: '';
		padding-bottom: 100%;
		display: block;
	}

	:deep(.q-uploader__header) {
		background-color: unset;
	}

	&__save {
		max-width: 250px;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 20px;
	}
}

.draggable {
	display: flex;
	position: relative;

	&:before {
		content: '';
		display: block;
	}

	&__area {
		width: 100%;
		height: 100%;
		position: absolute;
	}

	&__image-wrap {
		height: 100%;
	}

	&__image {
		top: 50%;
		left: 50%;
		max-width: 100%;
		max-height: 100%;
		position: absolute;
		vertical-align: bottom;
		transform: translate(-50%, -50%);
	}

	&_type_cup {
		width: 45.5%;
		margin-top: 7%;
		margin-left: 10%;

		&:before {
			padding-bottom: 114%;
		}
	}
}



@media screen and (max-width: 1023px) {
	.constructor {
		&__container {
			max-width: 80vw;
		}
	}
}



@media screen and (max-width: 599px) {
	.constructor {
		&__container {
			max-width: unset;
		}
	}
}
</style>
