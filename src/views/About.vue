<script setup>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import '../assets/main.css';
import '../assets/responsive.css';
import { Swiper, SwiperSlide } from "swiper/vue";
import { ref, computed, onUnmounted, onMounted} from "vue";
import "swiper/css";
import "swiper/css/pagination";
import "swiper/css/effect-fade";
import "swiper/css/navigation";
import { Navigation  } from "swiper/modules";
import AOS from "aos";
import "aos/dist/aos.css";

const message = "Hey,\n\n" +
  "I would like to inquire about your photography services"

const whatsappNumber = "447507971045"; // Replace with your WhatsApp number (remove +)
const whatsappLink = computed(() => {
  return `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(message)}`;
});


const showScrollTop = ref(false);

const testimonials = [
  {
    image: "/images/jpeg-optimizer_banner-img1.jpg",
    name: "BLESSING OGODOGU",
    role: "Software Developer and Founder",
    message:
      "The process was smooth, and the results were outstanding! He knew exactly how to bring out the best in each shot, and now my LinkedIn profile looks so much more professional!. Looking forward to working with Spac Studios again.",
  },
  {
    image: "/images/img36.jpg",
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

onMounted(() => {
  AOS.init();
});


</script>

<template>
  <div>
      <div>
         <Header />
      </div>
      <div class="page-section">
          <div class="page-title">
              <div>
                  <h4>
                     About Spac Studios
                  </h4>
              </div>
              <div>

              </div>
          </div>
      </div>
      <div class="aboutus-section">
          <div class="aboutus-container">
                <div class="about-us-text">
                  <p>
                    At Spac Studios, we believe that every picture tells a story. 
                    Our approach is simple: we blend creativity with technical 
                    expertise to deliver stunning, high-quality images. We take time to understand
                    our clients' vision, ensuring every shot reflects their personality, emotions, and special moments.
                  </p>
                  <div>
                     <h2>Our Commitment to Quality</h2>
                     <p>
                        We pride ourselves on delivering top-tier photography services. Whether it's a portrait session or a large-scale event, 
                        we ensure every detail is perfect. From high-resolution imagery to expert post-processing, we guarantee excellence in every frame.
                    </p>
                  </div>
                  <div>
                    <h2>State-of-the-Art Equipment</h2>
                    <p>
                        We are equipped with high-end cameras, professional lighting, and advanced editing tools to ensure superior image quality.
                        We stay updated with the latest photography trends and techniques, allowing us to provide the best experience for our clients.
                    </p>
                  </div>
                </div>
                <div class="about-us-image" data-aos="fade-up" data-aos-duration="2000">
                     <img src="/images/about-us.jpg">
                </div>
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
