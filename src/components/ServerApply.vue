<template>
  <section id="apply" class="py-16 bg-white">
    <div class="container mx-auto px-4">
      <div class="max-w-4xl mx-auto">
        <div class="text-center mb-12">
          <h2 class="text-[clamp(1.5rem,3vw,2.5rem)] font-bold text-dark mb-4">服务器入驻申请</h2>
          <p class="text-dark-2 max-w-2xl mx-auto">
            欢迎优质Minecraft服务器加入恒星MC社区，与更多玩家分享你的服务器
          </p>
        </div>

        <div class="grid md:grid-cols-2 gap-8">
          <!-- 申请表单 -->
          <div class="bg-light-1 rounded-xl p-8">
            <h3 class="text-xl font-semibold text-dark mb-6">填写申请信息</h3>
            <form @submit.prevent="submitApplication" class="space-y-6">
              <div>
                <label class="block text-sm font-medium text-dark-2 mb-2">服务器名称</label>
                <input
                  v-model="form.name"
                  type="text"
                  required
                  class="w-full px-4 py-2 rounded-lg border border-light-2 focus:outline-none focus:ring-2 focus:ring-primary/50"
                  placeholder="请输入服务器名称"
                />
              </div>

              <div>
                <label class="block text-sm font-medium text-dark-2 mb-2">服务器地址</label>
                <input
                  v-model="form.address"
                  type="text"
                  required
                  class="w-full px-4 py-2 rounded-lg border border-light-2 focus:outline-none focus:ring-2 focus:ring-primary/50"
                  placeholder="如: mc.example.com"
                />
              </div>

              <div>
                <label class="block text-sm font-medium text-dark-2 mb-2">服务器类型</label>
                <select
                  v-model="form.type"
                  required
                  class="w-full px-4 py-2 rounded-lg border border-light-2 focus:outline-none focus:ring-2 focus:ring-primary/50"
                >
                  <option value="">请选择类型</option>
                  <option value="survival">生存</option>
                  <option value="creative">创造</option>
                  <option value="rpg">RPG</option>
                  <option value="minigames">迷你游戏</option>
                  <option value="other">其他</option>
                </select>
              </div>

              <div>
                <label class="block text-sm font-medium text-dark-2 mb-2">服务器版本</label>
                <input
                  v-model="form.version"
                  type="text"
                  required
                  class="w-full px-4 py-2 rounded-lg border border-light-2 focus:outline-none focus:ring-2 focus:ring-primary/50"
                  placeholder="如: 1.20.1"
                />
              </div>

              <div>
                <label class="block text-sm font-medium text-dark-2 mb-2">服务器描述</label>
                <textarea
                  v-model="form.description"
                  required
                  rows="4"
                  class="w-full px-4 py-2 rounded-lg border border-light-2 focus:outline-none focus:ring-2 focus:ring-primary/50"
                  placeholder="请详细描述你的服务器特色和玩法"
                ></textarea>
              </div>

              <div>
                <label class="block text-sm font-medium text-dark-2 mb-2">联系方式</label>
                <input
                  v-model="form.contact"
                  type="text"
                  required
                  class="w-full px-4 py-2 rounded-lg border border-light-2 focus:outline-none focus:ring-2 focus:ring-primary/50"
                  placeholder="QQ/微信/邮箱"
                />
              </div>

              <button
                type="submit"
                :disabled="isSubmitting"
                class="w-full py-3 bg-primary hover:bg-primary/90 text-white font-medium rounded-lg transition-colors disabled:opacity-50"
              >
                {{ isSubmitting ? '提交中...' : '提交申请' }}
              </button>
            </form>

            <div
              v-if="submitStatus"
              class="mt-4 p-4 rounded-lg"
              :class="
                submitStatus.type === 'success'
                  ? 'bg-success/10 text-success'
                  : 'bg-danger/10 text-danger'
              "
            >
              {{ submitStatus.message }}
            </div>
          </div>

          <!-- 入驻须知 -->
          <div class="bg-light-1 rounded-xl p-8">
            <h3 class="text-xl font-semibold text-dark mb-6">入驻须知</h3>
            <div class="space-y-4 text-dark-2">
              <div class="flex items-start gap-3">
                <i class="fa fa-check-circle text-success mt-1"></i>
                <div>
                  <h4 class="font-medium text-dark">服务器质量要求</h4>
                  <p class="text-sm">服务器需要稳定运行，拥有良好的游戏环境和活跃的管理团队。</p>
                </div>
              </div>

              <div class="flex items-start gap-3">
                <i class="fa fa-check-circle text-success mt-1"></i>
                <div>
                  <h4 class="font-medium text-dark">内容合规</h4>
                  <p class="text-sm">服务器内容必须符合法律法规，禁止包含任何违规或不良信息。</p>
                </div>
              </div>

              <div class="flex items-start gap-3">
                <i class="fa fa-check-circle text-success mt-1"></i>
                <div>
                  <h4 class="font-medium text-dark">审核流程</h4>
                  <p class="text-sm">
                    我们会在1-3个工作日内完成审核，并通过提供的联系方式通知结果。
                  </p>
                </div>
              </div>

              <div class="flex items-start gap-3">
                <i class="fa fa-check-circle text-success mt-1"></i>
                <div>
                  <h4 class="font-medium text-dark">免费入驻</h4>
                  <p class="text-sm">恒星MC社区为优质服务器提供免费推广服务，不收取任何费用。</p>
                </div>
              </div>

              <div class="mt-6 p-4 bg-primary/10 rounded-lg">
                <h4 class="font-medium text-dark mb-2">联系方式</h4>
                <p class="text-sm">如有疑问，请联系管理员：</p>
                <p class="text-sm font-medium">QQ群: 123456789</p>
                <p class="text-sm font-medium">邮箱: admin@starmc.com</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface ApplicationForm {
  name: string
  address: string
  type: string
  version: string
  description: string
  contact: string
}

const form = ref<ApplicationForm>({
  name: '',
  address: '',
  type: '',
  version: '',
  description: '',
  contact: '',
})

const isSubmitting = ref(false)
const submitStatus = ref<{ type: 'success' | 'error'; message: string } | null>(null)

const submitApplication = async () => {
  isSubmitting.value = true
  submitStatus.value = null

  try {
    // 模拟API调用
    await new Promise((resolve) => setTimeout(resolve, 1500))

    // 模拟成功提交
    submitStatus.value = {
      type: 'success',
      message: '申请提交成功！我们会在1-3个工作日内完成审核并联系您。',
    }

    // 清空表单
    form.value = {
      name: '',
      address: '',
      type: '',
      version: '',
      description: '',
      contact: '',
    }
  } catch {
    submitStatus.value = {
      type: 'error',
      message: '提交失败，请稍后重试或联系管理员。',
    }
  } finally {
    isSubmitting.value = false
  }
}
</script>

<style scoped>
.text-dark {
  color: #1d2129;
}
.text-dark-2 {
  color: #4e5969;
}
.bg-light-1 {
  background-color: #f2f3f5;
}
.bg-light-2 {
  background-color: #e5e6eb;
}
.text-success {
  color: #00b42a;
}
.text-danger {
  color: #f53f3f;
}
</style>
