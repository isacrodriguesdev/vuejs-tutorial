
<template>
  <p>
    {{ user.name }}
  </p>
</template>

<script>

export default {
  name: 'MyUser',
  props: {
    user: Object,
  },
}

</script>

<style></style>