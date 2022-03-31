<template>
  <div id="date">sdsd
  </div>
  <div id="date2">
    {{date2}}
  </div>
</template>

<script>
export default {
  setup() {
    const date = Date().toString()
    return {
      date,
    }
  },
  date()  {
    return  {
      date2: Date().toString()
    }
  },
}
</script>