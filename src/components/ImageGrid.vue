<template>
  <div class="image-grid">
    <div v-for="(image, index) in images" :key="index" class="image-item">
      <img
        :src="image.src"
        :alt="image.alt"
        class="grid-image"
        @click="openPopup(image)"
      >
      <p class="image-text">{{ image.text }}</p>
    </div>

    <div v-if="showPopup" class="popup-overlay">
      <div class="popup">
        <button class="close-button" @click="closePopup">×</button>
        <img :src="selectedImage.src" alt="Popup Image" class="popup-image">
        <h3 class="popup-title">Comment</h3>
        <textarea
          class="popup-textarea"
          placeholder=" "
        ></textarea>
        <p class="popup-message">Write a few sentences about the photo.</p>
        <button class="popup-save-button">Save</button>
        <h3 class="popup-title">Comments</h3>
        <h3 class="popup-сomment">Author1: comment of the author</h3>
        <h3 class="popup-сomment">Author2: comment of the author</h3>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ImageGrid',
  data() {
    return {
      images: [
        { src: require('@/assets/image1.svg'), alt: 'Image 1', text: 'Текст 1' },
        { src: require('@/assets/image2.svg'), alt: 'Image 2', text: 'Текст 2' },
        { src: require('@/assets/image3.svg'), alt: 'Image 3', text: 'Текст 3' },
        { src: require('@/assets/image4.svg'), alt: 'Image 4', text: 'Текст 4' },
        { src: require('@/assets/image5.svg'), alt: 'Image 5', text: 'Текст 5' },
        { src: require('@/assets/image6.svg'), alt: 'Image 6', text: 'Текст 6' },
      ],
      showPopup: false,
      selectedImage: null,
    };
  },
  methods: {
    openPopup(image) {
      this.selectedImage = image;
      this.showPopup = true;
    },
    closePopup() {
      this.showPopup = false;
    },
  },
};
</script>

<style scoped>
.image-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  padding: 0 0 24px 0;
}

.image-item {
  text-align: center;
}

.grid-image {
  width: 431px;
  height: 216px;
  object-fit: cover;
  border-radius: 10px;
  cursor: pointer;
}

.image-text {
  color: black;
  margin-top: 10px;
  font-size: 14px;
  display: flex;
  justify-content: start;
  padding-left: 2%;
}

.popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.popup {
  width: 693px;
  max-height: 90vh; /* Ограничиваем высоту модального окна */
  background: white;
  border-radius: 10px;
  padding: 20px;
  position: relative;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  overflow-y: auto; /* Добавляем скролл для модального окна */
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 24px;
  cursor: pointer;
  color: #333;
}

.close-button:hover {
  color: #000;
}

.popup-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.popup-image {
  width: 405px;
  height: 405px;
  object-fit: cover;
  border-radius: 10px;
}

.popup-title {
  display: flex;
  padding: 2%;
  margin: 0;
  margin-top: 2%;
  font-size: 14px;
  font-weight: bold;
  color: #374151;
}

.popup-сomment {
  display: flex;
  padding: 1% 2%;
  margin: 0;
  margin-top: 2%;
  font-size: 14px;
  font-weight: bold;
  color: #000;
}

.popup-textarea {
  width: 95%;
  min-height: 100px;
  max-height: 300px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  resize: vertical;
  overflow-y: auto;
}

.popup-message {
  display: flex;
  padding: 0 2%;
  margin: 0;
  margin-top: 1%;
  font-size: 14px;
  color: #6B7280;
}

.popup-save-button {
  padding: 10px 20px;
  background-color: #4F46E5;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 3%;
}

.popup-save-button:hover {
  background-color: #0056b3;
}
</style>