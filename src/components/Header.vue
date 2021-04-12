<template>

    <header>
        <h1>My songs</h1>    
    </header>

</template>
<script>


export default{
    name:'Header'
}
</script>

<style scoped>
header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background: rgba(0, 0, 0, 0.897);
  color:#fff;
  box-shadow: 2px 4px 2px 4px rgba(0, 0, 0, 0.1);
  border-bottom: 2px solid rgba(0, 0, 0, 0.2);
  margin-bottom: 20px;
}
</style>