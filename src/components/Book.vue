<template>
  <div>
    <image src="http://placeimg.com/480/640/any" alt="Book cover image" />
    <div>Title: {{ title }}</div>
    <div>Author: {{ author }}</div>
  </div>
</template>

<script>
export default {
  name: "Book",
  props: {
    title: String,
    author: String,
  },
};
</script>
