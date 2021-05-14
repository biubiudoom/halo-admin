<template>
	<page-view>
		<a-row :gutter="12">
			<a-col :xl="10" :lg="10" :md="10" :sm="24" :xs="24" class="pb-3">
				<a-card :title="title" :bodyStyle="{ padding: '16px' }">
					<a-form-model ref="categoryForm" :model="form.model" :rules="form.rules" layout="horizontal">
					  <a-form-model-item label="名称：" prop="name">
					    <a-input v-model="form.model.name" />
					  </a-form-model-item>
					  <a-form-model-item label="简介："  prop="slug">
					    <a-input v-model="form.model.slug" />
					  </a-form-model-item>
					  <a-form-model-item label="使用说明：" help="* 介绍功能" prop="thumbnail">
					    <a-input v-model="form.model.thumbnail">
					      <a href="javascript:void(0);" slot="addonAfter" @click="thumbnailDrawer.visible = true">
					        <a-icon type="picture" />
					      </a>
					    </a-input>
					  </a-form-model-item>
					  <!-- <a-form-model-item label="密码：" help="* 分类密码" prop="password">
					    <a-input-password v-model="form.model.password" autocomplete="new-password" />
					  </a-form-model-item>
					  <a-form-model-item label="描述：" help="* 分类描述，需要主题支持" prop="description">
					    <a-input type="textarea" v-model="form.model.description" :autoSize="{ minRows: 3 }" />
					  </a-form-model-item> -->
					  <a-form-model-item>
					    <ReactiveButton
					      v-if="!isUpdateMode"
					      type="primary"
					      @click="handleCreateOrUpdateCategory"
					      @callback="handleSavedCallback"
					      :loading="form.saving"
					      :errored="form.errored"
					      text="保存"
					      loadedText="保存成功"
					      erroredText="保存失败"
					    ></ReactiveButton>
					    <a-button-group v-else>
					      <ReactiveButton
					        type="primary"
					        @click="handleCreateOrUpdateCategory"
					        @callback="handleSavedCallback"
					        :loading="form.saving"
					        :errored="form.errored"
					        text="更新"
					        loadedText="更新成功"
					        erroredText="更新失败"
					      ></ReactiveButton>
					      <a-button type="dashed" @click="form.model = {}">返回添加</a-button>
					    </a-button-group>
					  </a-form-model-item>
					</a-form-model>
					</a-card>
			</a-col>
		</a-row>
	</page-view>
</template>

<script>
	import { PageView } from '@/layouts'
	export default {
	  components: {
	    PageView
	  },
		data() {
			return {
				form: {
				  model: {},
				  saving: false,
				  errored: false,
				  rules: {
				    name: [
				      { required: true, message: '* 分类名称不能为空', trigger: ['change'] },
				      { max: 255, message: '* 分类名称的字符长度不能超过 255', trigger: ['change'] }
				    ],
				    slug: [{ max: 255, message: '* 分类别名的字符长度不能超过 255', trigger: ['change'] }],
				    thumbnail: [{ max: 1023, message: '* 封面图链接的字符长度不能超过 1023', trigger: ['change'] }],
				    description: [{ max: 100, message: '* 分类描述的字符长度不能超过 100', trigger: ['change'] }]
				  }
				},
			}
		}
	}
</script>

<style>
</style>
