<template>
  <div class="user-profile-container">
    <div class="user-profile">
      <div class="left-block">
        <img src="@/assets/avatar.svg" alt="Avatar" class="avatar">
        <span class="name">Ricardo Cooper</span>
      </div>
      <div class="right-block">
        <button class="button primary">Message</button>
        <button class="button secondary">Call</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UserProfile',
};
</script>

<style scoped>
.user-profile-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.user-profile {
  width: 1024px;
  height: 128px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  position: relative;
  margin-top: -134px;
}

.left-block {
  display: flex;
  align-items: center; 
  gap: 20px; 
}

.avatar {
  width: 128px;
  height: 128px;
  border-radius: 50%;
  object-fit: cover;
  position: absolute;
  top: -40px;
  left: 20px; 
}

.name {
  font-size: 24px;
  color: #000;
  font-weight: 700;
  margin-left: 148px; 
}

.right-block {
  display: flex;
  gap: 10px; 
  align-items: center;
}

.button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
}

.primary {
  width: 119px;
  height: 38px;
  background-color: white;
  color: black;
}

.secondary {
  width: 84px;
  height: 38px;
  background-color: white;
  color: black;
}

/* Медиазапрос для мобильных устройств */
@media (max-width: 1355px) {
  .user-profile {
    width: 100%;
    flex-direction: column;
    align-items: center;
    height: auto;
    margin-top: 0;
    padding: 20px;
  }

  .left-block {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    margin-top: -40px;
  }

  .avatar {
    width: 100px;
    height: 100px;
    position: relative;
    top: 0;
    margin-right: 30px;
  }

  .name {
    font-size: 18px;
    margin-left: 0;
    margin-top: 10px;
  }

  .right-block {
    display: flex;
    flex-direction: column;
    gap: 10px;
    align-items: center;
    margin-top: 20px;
  }

  .button {
    width: 100%;
    max-width: 150px;
    font-size: 16px;
    padding: 12px;
  }

  .primary {
    width: 100%;
  }

  .secondary {
    width: 100%;
  }
}
</style>
