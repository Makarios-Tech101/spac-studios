<script setup>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import '../assets/main.css';
import { ref, computed, watchEffect, onMounted, onUnmounted } from "vue";
// import { Swiper, SwiperSlide } from "swiper/vue";
// import "swiper/css";
// import "swiper/css/pagination";
// import "swiper/css/effect-fade";
// import "swiper/css/navigation";
import AOS from "aos";
import "aos/dist/aos.css";

const message = "Hey,\n\n" +
  "I would like to inquire about your photography services"

const whatsappNumber = "447507971045"; // Replace with your WhatsApp number (remove +)
const whatsappLink = computed(() => {
  return `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(message)}`;
});


const galleries = ref([
  { src: "/images/service1.JPG", title: "Birthday Shoot" },
  { src: "/images/jpeg-optimizer_banner-img1.jpg", title: "Headshot" },
  { src: "/images/banner-img5.jpg", title: "Studio Shoot" },
  { src: "/images/img1.jpg", title: "Event Shoot" },
  { src: "/images/img18.JPG", title: "Family Portrait" },
  { src: "/images/img19.jpg", title: "Child Photography" },
  { src: "/images/img20.jpg", title: "Child Photography" },
  { src: "/images/img_book.jpg", title: "Fashion Photography" },
  { src: "/images/service2.JPG", title: "Child Photography" },
  { src: "/images/img11.JPG", title: "Studio Shoot" },
  { src: "/images/img25.jpg", title: "Headshot" },
  { src: "/images/img8.JPG", title: "Fashion Photography" },
  { src: "/images/img12.JPG", title: "Studio Shoot" },
  { src: "/images/img14.jpg", title: "Birthday Shoot" },
  { src: "/images/img15.JPG", title: "Fashion Photography" },
  { src: "/images/img17.jpg", title: "Birthday Shoot" },
  { src: "/images/img21.jpg", title: "Child Photography" },
  { src: "/images/img14.jpg", title: "Fashion Photography" },
  { src: "/images/service3.jpg", title: "Child Photography" },
  { src: "/images/jpeg-optimizer_banner-img2.jpg", title: "Child(ren) Photography" },
  { src: "/images/img9.jpg", title: "Fashion Photography" },
  { src: "/images/img10.jpg", title: "Fashion Photography" },
  { src: "/images/img23.JPG", title: "Outdoor Shoot" },
  { src: "/images/img23.JPG", title: "Headshot" },
  { src: "/images/img15.JPG", title: "Fashion Photography" },
  
]);


const selectedImage = ref(null);
const selectedTitle = ref(null);
const showScrollTop = ref(false);

const openModal = (image) => {
  selectedImage.value = image.src;
  selectedTitle.value = image.title;
};

const closeModal = () => {
  selectedImage.value = null;
  selectedTitle.value = null;
};

onMounted(() => {
  AOS.init();
});



const handleScroll = () => {
  showScrollTop.value = window.scrollY > 200; // Show button after scrolling 200px
};

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: "smooth" });
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});

</script>

<template>
    <div>
        <div>
           <Header />
        </div>
        <div class="gallery-section">
            <div class="gallery-title">
                <div>
                    <h4>
                       Gallery
                    </h4>
                </div>
                <div>

                </div>
            </div>
            <div class="gallery-container">
                <div class="gallery" >
                    <img 
                    v-for="(gallery, index) in galleries" 
                    :key="index"
                    :src="gallery.src" 
                    :alt="gallery.title"
                    alt="Gallery Image" 
                    class="gallery-item" 
                    @click="openModal(gallery)"
                    :class="{'tall': index % 5 === 0, 'wide': index % 7 === 0}"
                    data-aos="fade-up" data-aos-duration="2000"
                    
                    />
                </div>
            </div>
        </div>
        <!-- Modal -->
        <div v-if="selectedImage" class="modal" @click="closeModal">
            <div class="modal-content" @click.stop>
                <button class="close-button" @click="closeModal">&times;</button>
                <img 
                  :src="selectedImage" 
                  alt="Modal Image" 
                  class="modal-image"
                >
                <h3 class="modal-title">{{ selectedTitle }}</h3> 
            </div>
        </div>
        <div>
          <Footer />
        </div>
       <!-- WhatsApp Floating Button -->
        <div>
            <a :href="whatsappLink" target="_blank" class="whatsapp-button">
                <img src="/images/WhatsApp_icon.png" alt="WhatsApp">
            </a>
        </div>  
        <div>
        <!-- Scroll to Top Button -->
            <button v-if="showScrollTop" @click="scrollToTop" class="scroll-top-button">
                ↑
            </button>
        </div>  
    </div>
   
</template>