<script>
import IconFile from './IconFile'
import IconFolder from './IconFolder'
import IconFolderOpen from './IconFolderOpen'

export default {
  props: {
    files: { type: Array, default: () => [] }
  },
  components: { IconFile, IconFolder, IconFolderOpen },
  setup(_, { emit }) {
    const onFileClick = file => {
      if (file.directory) emit('folderclick', file)
    }
    return { onFileClick }
  }
}
</script>

<template>
  <table class="table">
    <tbody>
      <tr class="clickable" @click="$emit('back')">
        <td class="icon-row">
          <IconFolderOpen class="icon-folder" />
        </td>
        <td>...</td>
        <td></td>
      </tr>

      <tr
        v-for="file in files"
        :key="file.name"
        :class="{ clickable: file.directory }"
        @click="onFileClick(file)"
      >
        <td class="icon-row">
          <IconFolder v-if="file.directory" class="icon-folder" />
          <IconFile v-else class="icon-file" />
        </td>
        <td>{{ file.name }}</td>
        <td>
          <span class="float-end">{{ file.size }}</span>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
.clickable {
  cursor: pointer;
}

.icon-row {
  width: 2em;
}
.icon-folder {
  width: 1em;
}
.icon-file {
  width: 0.75em;
}
</style>
