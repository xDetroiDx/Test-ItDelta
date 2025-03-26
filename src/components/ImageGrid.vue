<template>
  <div class="image-grid-wrapper">
    <div v-if="loading" class="loading">Loading...</div>
    <div v-if="error" class="error">{{ error }}</div>

    <div class="image-grid">
      <div v-for="image in images" :key="image.id" class="image-item">
        <img 
          :src="image.image" 
          :alt="'Image ' + image.id" 
          class="grid-image"
          @click="openPopup(image.id)"
        >
        <p class="image-text">id:{{ image.id }}</p>
      </div>
      
      <div v-if="showPopup" class="popup-overlay">
        <div class="popup">
          <button class="close-button" @click="closePopup">×</button>
          <img v-if="popupData.image" :src="popupData.image" alt="Popup Image" class="popup-image">
          <div v-else class="image-loading">Loading image...</div>
          
          <h3 class="popup-title">Comment</h3>
          <textarea
            class="popup-textarea"
            placeholder=""
            v-model="newComment"
          ></textarea>
          <p class="popup-message">Write a few sentences about the photo.</p>
          
          <button 
            class="popup-save-button" 
            @click="saveComment"
            :disabled="isSavingComment || !newComment.trim()"
          >
            {{ isSavingComment ? 'Saving...' : 'Save' }}
          </button>
          
          <div v-if="commentError" class="comment-error">
            <strong>Error:</strong> {{ commentError }}
          </div>
          
          <h3 class="popup-title">Comments</h3>
          <div v-if="popupData.comments && popupData.comments.length">
            <div v-for="comment in popupData.comments" :key="comment.id" class="popup-comment">
              <strong>{{ comment.author || 'Anonymous' }}:</strong> {{ comment.text }}
            </div>
          </div>
          <div v-else class="no-comments">No comments yet</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'ImageGrid',
  data() {
    return {
      images: [],
      loading: true,
      error: null,
      showPopup: false,
      popupData: {
        image: null,
        comments: []
      },
      currentImageId: null,
      newComment: '',
      isSavingComment: false,
      commentError: null
    };
  },
  methods: {
    async openPopup(imageId) {
      this.currentImageId = imageId;
      this.showPopup = true;
      this.popupData = { image: null, comments: [] };
      this.commentError = null;
      this.newComment = '';
      
      try {
        const response = await axios.get(`http://test-backend.itdelta.agency/api/image/${imageId}`);
        this.popupData = {
          image: response.data.image,
          comments: response.data.comments || []
        };
      } catch (err) {
        this.error = 'Error loading image data: ' + err.message;
      }
    },
    closePopup() {
      this.showPopup = false;
    },
    async saveComment() {
      if (!this.newComment.trim()) return;

      this.isSavingComment = true;
      this.commentError = null;

      try {
        const response = await axios.post(
          `http://test-backend.itdelta.agency/api/image/${this.currentImageId}/comments`,
          {
            comment: this.newComment
          },
          {
            headers: {
              'Content-Type': 'application/json'
            }
          }
        );

        console.log('Comment POST response status:', response.status);
        
        if (response.data) {
          this.popupData.comments.unshift({
            id: Date.now(),
            text: this.newComment,
            author: "Anonymous"
          });
        }
        
        this.newComment = '';
      } catch (error) {
        console.log('Comment POST error status:', error.response?.status);
        if (error.response) {
          this.commentError = error.response.data.message || 'Failed to save comment';
        } else {
          this.commentError = error.message;
        }
      } finally {
        this.isSavingComment = false;
      }
    }
  },
  async created() {
    try {
      const response = await axios.get('http://test-backend.itdelta.agency/api/images');
      this.images = response.data;
    } catch (err) {
      this.error = 'Error loading images: ' + err.message;
    } finally {
      this.loading = false;
    }
  }
};
</script>

<style scoped>
.image-grid-wrapper {
  max-width: 1400px;
  margin: 0 auto;
}

.image-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  padding: 0 0 24px 0;
}

.image-item {
  text-align: center;
  cursor: pointer;
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

.loading, .error {
  text-align: center;
  font-size: 18px;
  color: #333;
  padding: 20px;
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
  max-height: 90vh;
  background: white;
  border-radius: 10px;
  padding: 20px;
  position: relative;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  overflow-y: auto;
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

.popup-comment {
  display: flex;
  padding: 8px 16px;
  margin: 4px 0;
  color: #000;
  border-radius: 4px;
  font-size: 14px;
}

.no-comments {
  padding: 16px;
  color: #000;
  text-align: center;
}

.image-loading {
  width: 405px;
  height: 405px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f5f5f5;
  border-radius: 10px;
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
  transition: background-color 0.3s;
}

.popup-save-button:hover:not(:disabled) {
  background-color: #4338CA;
}

.popup-save-button:disabled {
  background-color: #9CA3AF;
  cursor: not-allowed;
}

.comment-error {
  color: #DC3545;
  margin-top: 10px;
  padding: 10px;
  background-color: #F8D7DA;
  border-radius: 4px;
  font-size: 14px;
}

/* Медиазапросы для мобильных устройств */
@media (max-width: 768px) {
  .image-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
  }

  .grid-image {
    width: 100%;
    height: auto;
  }

  .popup {
    width: 90%;
    max-height: 80vh;
    padding: 10px;
  }

  .popup-image {
    width: 100%;
    height: auto;
  }

  .popup-textarea {
    width: 100%;
  }

  .popup-save-button {
    width: 100%;
  }
}
</style>
