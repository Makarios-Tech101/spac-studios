<script setup>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import '../assets/main.css';
import '../assets/responsive.css';
import { ref, computed, onMounted, onUnmounted } from "vue";
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
import 'swiper/css/navigation';
import { Navigation } from 'swiper/modules';
import AOS from "aos";
import "aos/dist/aos.css";

const message = "Hey,\n\n" +
  "I would like to inquire about your photography services"

const whatsappNumber = "447507971045"; // Replace with your WhatsApp number (remove +)
const whatsappLink = computed(() => {
  return `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(message)}`;
});


const showScrollTop = ref(false);
const pricingPlans = ref([
  {
    title: "LITE PACKAGE",
    price: "£70",
    // per: "/ H",
    features: [
      { text: "Corporate Headshots", available: true },
      { text: "45 mins Shoot ", available: true },
      { text: "1 Outfit ", available: true },
      { text: "3 Hi-Res Retouched Images ", available: true },
      { text: "1 individual", available: true },
      { text: "Digital Access To Image Files ", available: true },
    ],
  },
  {
    title: "CLASSIC PACKAGE",
    price: "£220",
    // per: "/ H",
    features: [
      { text: "Studio | Birthday | Outdoor ", available: true },
      { text: "⁠90 mins Shoot", available: true },
      { text: "Up to 2 Outfits", available: true },
      { text: "8 Hi-Res Retouched Images ", available: true },
      { text: "1 Individual ", available: true },
      { text: "Digital Access To Image Files", available: true },
    ],
  },
  {
    title: "DELUXE PACKAGE",
    // subtitle: "EQUIPMENTS & ASSISTANTS",
    price: "£350",
    // per: "/ H",
    features: [
      { text: "Family Shoot", available: true },
      { text: "120 mins Shoot", available: true },
      { text: "Up To 3 Outfits", available: true },
      { text: "16 Hi-Res Retouched Images", available: true },
      { text: "Up To 4 Individuals", available: true },
      { text: "Extra £30 For 4+ Individuals", available: true },
      { text: "⁠Styling & Posing Guide", available: true },
      { text: "Digital access to image files", available: true },
    ],
  },
  {
    title: "EVENT PACKAGE",
    price: "1st Hour £120",
    // per: "/ H",
    features: [
      { text: "15 Edited Photos Per Hour", available: true },
      { text: "Additional hour £80", available: true },
    ],
  },
  {
    title: "ADDITIONAL CHARGES",
    // price: "$99",
    // per: "/ H",
    features: [
      { text: "Travel Fee For Home Shoot - Beyond 10 Mile Radius ", available: true },
      { text: "Extra Edited Images @£20", available: true },
      { text: "30+ Digital Unedited Images @£30", available: true },
      { text: "All Photos Sent Via Free Download Link. USB Delivered Images Attracts Extra @£20 Charge", available: true },
      { text: "Additional Charges Will Be Incurred For Time Extension Beyond Agreed Hours", available: true },
    ],
  },
]);

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
                     Pricing
                  </h4>
              </div>
              <div>

              </div>
          </div>
      </div>
      <div class="pricing-page-section">
        <div class="pricing-page-container">
            <swiper
                :modules="[Navigation]"
                :navigation="true"
                :slides-per-view="1"
                :space-between="20"
                class="pricing-swiper"
                :breakpoints="{
                    992: { slidesPerView: 1 },
                    1024: { slidesPerView: 3 },
                }"
            >
                <swiper-slide v-for="(plan, index) in pricingPlans" :key="index">
                    <div class="pricing-card" :class="{ highlighted: index === 2 }">
                    <h3 class="pricing-title">{{ plan.title }}</h3>
                    <p class="pricing-subtitle">{{ plan.subtitle }}</p>
                    <div class="pricing-cost">
                        <span class="price" >{{ plan.price }}</span>
                        <span class="per">{{ plan.per }}</span>
                    </div>
                    <ul class="pricing-features" :class="{ highheighted: index === 4 }">
                        <li v-for="(feature, i) in plan.features" :key="i">
                        <span v-if="feature.available">✔</span>
                        <span v-else>✖</span>
                        {{ feature.text }}
                        </li>
                    </ul>
                    <!-- <button class="pricing-button" :class="{ highlight : index === 2 }"> -->
                        <a :href="whatsappLink"
                          target="_blank" 
                          class="pricing-button" 
                          :class="{ highlight : index === 2 }">
                          Book Now
                        </a>
                    <!-- </button> -->
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
