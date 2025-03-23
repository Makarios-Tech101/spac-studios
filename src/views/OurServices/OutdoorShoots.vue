<script setup>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import '../../assets/main.css';
import { ref, computed, onMounted, onUnmounted } from "vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/pagination";
import "swiper/css/effect-fade";
import "swiper/css/navigation";
import { Autoplay, Pagination, EffectFade, Navigation  } from "swiper/modules";
import AOS from "aos";
import "aos/dist/aos.css";

const message = "Hello! Thank you for contacting Spac Studios.\n\n" +
  "How can we help you today?\n\n" +
  "Please select the type of photography service you're interested in:\n" +
  "1 Portraits & Headshots\n" +
  "2 Wedding & Events\n" +
  "3 Birthday Shoots\n" +
  "4 Child Photography\n" +
  "5 Corporate Events\n" +
  "6 Fashion Photography\n" +
  "7 Outdoor Shoots\n" +
  "8 Product Photography\n\n" +
  "Kindly reply with the number (1-8) of your preferred service, and we'll guide you through the booking process. We look forward to capturing your special moments! ";

const whatsappNumber = "447507971045"; // Replace with your WhatsApp number (remove +)
const whatsappLink = computed(() => {
  return `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(message)}`;
});

const serviceImages= ref([
   { src: "/images/img5.JPG",},
   { src: "/images/img23.JPG",}
]);

const testimonials = [
  {
    image: "/images/jpeg-optimizer_banner-img1.jpg",
    name: "BLESSING OGODOGU",
    role: "Software Developer and Founder",
    message:
      "The process was smooth, and the results were outstanding! He knew exactly how to bring out the best in each shot, and now my LinkedIn profile looks so much more professional!. Looking forward to working with Spac Studios again.",
  },
  {
    image: "/images/img3.jpg",
    name: "FEMI OYEBADE",
    role: "Auditor",
    message:
      "We had a wonderful experience during our family shoot. The photographer was so patient with our little ones, and the final pictures were heartwarming. These are moments we’ll treasure forever",
  },
  {
    image: "/images/img_book.jpg",
    name: "DEBBY",
    role: "Student",
    message:
      "I wanted some professional portraits, and he completely exceeded my expectations. The lighting, the angles, and the editing were all top-notch. I have never felt more confident in front of a camera!",
  },
  // {
  //   image: "/images/img1.jpg",
  //   name: "PASCAL EKEH",
  //   role: "Senior Advocate, Deloitte",
  //   message:
  //     "For one who approached Spac Studios unprepared, I got the support I needed. ",
  // }
];

const selectedImage = ref(null);
const showScrollTop = ref(false);

const openModal = (serviceImage) => {
  selectedImage.value = serviceImage;
};

const closeModal = () => {
  selectedImage.value = null;
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
      <div class="individual-services-banner-section">
        <div class="our-services-gallery-title">
              <div>
                  <h4>
                     Outdoor Shoots
                  </h4>
              </div>
              <div>

              </div>
          </div>
         <div class="individual-services-banner-container">
            <div class="individual-services-banner-content">
               <p>
                 Experience the beauty of natural light 
                 and scenic locations with our outdoor 
                 photography sessions. Whether for 
                 personal portraits, couple shoots, 
                 or adventure photography, we capture 
                 stunning imagery in breathtaking settings.
                 Session Options can include: Beach, park, and urban shoots,
                 Adventure and nature photography, Couples & solo outdoor portraits.
               </p>
               <p id="second-paragraph">
                    Enjoy a relaxed and enjoyable shoot while we take care of the creative details.
               </p>
               <a :href="whatsappLink" target="_blank">
                    Book Now
               </a>
            </div>
            <div>
  
            </div>
         </div>
      </div>
      <div class="our-services-gallery-container" id="our-services-gallery">
          <div class="our-services-gallery-grid-container">
                <div 
                    v-for="(serviceImage, index) in serviceImages" 
                    :key="index" 
                    class="our-services-gallery-grid" 
                    @click="openModal(serviceImage)"
                    data-aos="fade-up" data-aos-duration="2000"
                >
                    <img :src="serviceImage.src" alt=" Image" class="serviceImages">
            </div>   
          </div> 
      </div>
      <!-- Modal -->
      <div v-if="selectedImage" class="modal" @click="closeModal">
        <div class="modal-content" @click.stop>
          <button class="close-button" @click="closeModal">&times;</button>
          <img :src="selectedImage.src" alt="Modal Image" class="modal-image">
        </div>
      </div>
      <div class="testimonial-section">
       <div class="testimonial-title">
          <div>
            <h4>
              Testimonial
            </h4>
          </div>
          <div>

          </div>
       </div>
       <div class="testimonial-container">
        <swiper
            :modules="[Navigation]"
            :slides-per-view="1"
            :space-between="30"
            :navigation="true"
            :breakpoints="{
              992: { slidesPerView: 1 },
              1024: { slidesPerView: 2 },
            }"
            class="testimonial-slider"
          >
          <swiper-slide v-for="(testimonial, index) in testimonials" :key="index">
            <div class="mobile-testimonial">
              <img :src="testimonial.image" alt="Testimonial" id="profile-pic" />
            </div>
            <div class="testimonial-card">
              <div class="desktop-testimonial">
                <img :src="testimonial.image" alt="Testimonial" class="profile-pic" />
              </div>
              <div class="testimonial-content">
                <h3>{{ testimonial.name }}</h3>
                <h4>{{ testimonial.role }}</h4>
                <p>{{ testimonial.message }}</p>
              </div>
            </div>
          </swiper-slide>
        </swiper>
       </div>
      </div>
      <div class="contact-section">
        <div class="contact-map">
          <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d974.2128380875566!2d0.2846544288050937!3d51.50584081119247!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47d8b7525c0642ad%3A0xd5dbb89871591993!2sDanbury%20Cres%2C%20South%20Ockendon%2C%20UK!5e0!3m2!1sen!2sng!4v1742444094437!5m2!1sen!2sng" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
        </div>
        <div class="contact-details">
          <h4>Reach Out To Us</h4>
          <h6>Danbury Crescent, South Ockendon. RM15 5XF Essex Uk</h6>
          <p>+44 7507 971045</p>
          <!-- <p>info@spacstudios.co.uk</p> -->
          <router-link to="/contact">
            <button>Contact Form</button>
         </router-link>
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
