<script setup>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import '../assets/main.css';
import '../assets/responsive.css';
import { ref, onMounted, onUnmounted } from "vue";
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
import 'swiper/css/navigation';
import { Navigation } from 'swiper/modules';
import AOS from "aos";
import "aos/dist/aos.css";



const showScrollTop = ref(false);
const pricingPlans = ref([
  {
    title: "LITE PACKAGE",
    price: "£70",
    // per: "/ H",
    features: [
      { text: "1 Hour Shoot", available: true },
      { text: "1 Cloth", available: true },
      { text: "3 High-Res Retouched Images", available: true },
      { text: "Styling & Posing Guide ", available: true },
      { text: "One Person", available: true },
    ],
  },
  {
    title: "CLASSIC PACKAGE",
    price: "£150",
    // per: "/ H",
    features: [
      { text: "1 - 2 Hour Shoot", available: true },
      { text: "2 Cloths Change ", available: true },
      { text: "7 Hi-Res Retouched Images", available: true },
      { text: "Styling & Posing Guide", available: true },
      { text: "Up To 2 Persons", available: true },
    ],
  },
  {
    title: "DELUXE PACKAGE",
    // subtitle: "EQUIPMENTS & ASSISTANTS",
    price: "£250",
    // per: "/ H",
    features: [
      { text: "2 Hours Shoot ", available: true },
      { text: "3 Cloths Change", available: true },
      { text: "12 Hi-Res Retouched Images  ", available: true },
      { text: "Styling & Posing Guide", available: true },
      { text: "Up To 4 Persons ", available: true },
      { text: "£30 For Every Additional Person", available: true },
    ],
  },
  {
    title: "EVENT PACKAGE",
    price: "1st Hour £150",
    // per: "/ H",
    features: [
      { text: "15 Edited Photos Per Hour", available: true },
      { text: "Additional hour £70", available: true },
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
                        <a href="https://wa.me/447507971045" 
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
                <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d9905.016569687965!2d-0.19122115409877188!3d51.636870671592575!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x487619cc3ef6a4a1%3A0x518034b5f7d00bad!2sBuckingham%20Ave%2C%20London%2C%20UK!5e0!3m2!1sen!2sng!4v1740335035232!5m2!1sen!2sng"  style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade">
                </iframe>
            </div>
            <div class="contact-details">
                <h4>Reach Out To Us</h4>
                <h6>456 Main street, Buckingham Av. XV34 London</h6>
                <p>+44 7507 971045</p>
                <p>info@spacstudios.co.uk</p>
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
          <a href="https://wa.me/447507971045" target="_blank" class="whatsapp-button">
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
