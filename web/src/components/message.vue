<script setup lang="ts">
import { message as messageTip } from 'ant-design-vue'
import { CopyOutlined } from '@ant-design/icons-vue'
import { useClipboard } from '@vueuse/core'

const { copy } = useClipboard({})
type Message = {
  msg: string;
  username: string;
  time: string;
  type: number;
}
defineProps<{
  message: Message;
}>()

const copyIt = (msg: string) => {
  copy(msg)
  messageTip.success('Copied')
}
</script>

<template>
  <div class="my-2 self-end flex items-center flex-row" v-if="message.type === 1">
    <CopyOutlined class="pr-2 cursor-pointer self-end !text-gray-400" @click="copyIt(message.msg)" />
    <div class="p-1 rounded-t-lg rounded-l-lg bg-white shadow text-sm min-w-60 max-w-500">
      <a-textarea class="a" :value="message.msg" :auto-size="{ minRows: 1 }" :bordered="false" />
    </div>
  </div>
  <div class="my-2 self-start flex items-center" v-else>
    <div class="p-1 rounded-t-lg rounded-r-lg bg-blue-400 text-white shadow text-sm min-w-180 max-w-500">
      <a-textarea class="b" :value="message.msg" :auto-size="{ minRows: 1 }" :bordered="false" />
    </div>
    <CopyOutlined class="pl-2 cursor-pointer self-end !text-gray-400" @click="copyIt(message.msg)" />
  </div>
</template>

<style scoped>
.ant-card-body {
  padding: 5px !important;
}

.a {
  color: black;
  background-color: white;
}

.b {
  color: white;
  background-color: rgba(96, 165, 250, var(--un-bg-opacity));
}
</style>
