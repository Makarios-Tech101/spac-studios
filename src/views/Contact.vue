<script setup>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import '../assets/main.css';
import '../assets/responsive.css';
import { ref, computed, onUnmounted, onMounted} from "vue";
import AOS from "aos";
import "aos/dist/aos.css";

// const name = ref("");
// const email = ref("");
// const phone = ref("");
// const message = ref("");
// const selectedShootType = ref("");
// const shootDate = ref("");
const selectedReferral = ref("");
// const otherReferral = ref(""); 
const successMessage = ref("");
const errorMessage = ref("");
const isLoading = ref(false);
const showScrollTop = ref(false);


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


// Available shoot types
// const shootTypes = [
//     "Portraits & Headshots",
//     "Wedding & Events",
//     "Birthday Shoots",
//     "Child Photography",
//     "Corporate Events",
//     "Fashion Photography",
//     "Outdoor Shoots",
//     "Product Photography"
// ];

// Referral options
// const referralOptions = [
//     "Social Media (Instagram, Facebook, Twitter)",
//     "Google Search",
//     "Friend/Family Referral",
//     "Photography Event",
//     "Other"
// ];

const formData = ref({
  name: "",
  email: "",
  phone: "",
  shootType: "",
  shootDate: "",
  referral: "",
  // otherReferral: "",
  message: "",

});

const submitForm = async () => {
    isLoading.value = true;
    successMessage.value = "";
    errorMessage.value = "";
    
    const formDataObj = new FormData();
    Object.entries(formData.value).forEach(([key, value]) => {
        formDataObj.append(key, value);
    });

    formDataObj.append("_captcha", "false");
    formDataObj.append("_template", "table");

    try {
        const response = await fetch('https://formsubmit.co/oluspacko1@gmail.com', {
            method: 'POST',
            body: formDataObj,
        });

        if (response.ok) {
            successMessage.value = "Form submitted successfully!";
            formData.value = { name: '', email: '', phone: '', shootType: '', shootDate: '', referral: '', message: '' };
        } else {
            errorMessage.value = "There was an error submitting the form.";
        }
    } catch (error) {
        errorMessage.value = "An error occurred.";
    } finally {
        isLoading.value = false;
    }
};




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
                     Contact Us
                  </h4>
              </div>
              <div>

              </div>
          </div>
      </div>
      <div class="contactus-section">
          <div class="contactus-container">
                <div class="contact-us-text">
                  <p>
                    We are glad to have you!
                    Kindly fill out the contact form below and we will get back to your shortly.
                  </p>
                  <p>
                     Fields marked with an <span class="red"> * </span> are required
                  </p>
                  <form @submit.prevent="submitForm">
                    <input type="hidden" name="_captcha" value="false"> 
                    <input type="hidden" name="_next" value="#">
                    <div class="contact-form">
                        <label for="name">Name<span class="red"> * </span></label>
                        <input type="text" v-model="formData.name" placeholder="Your Name" required>
                    </div>
                    <div class="contact-form">
                        <label for="email">Email<span class="red"> * </span></label>
                        <input type="email" v-model="formData.email" placeholder="Your Email" required>
                    </div>
                    <div class="contact-form">
                        <label for="phone">Phone Number<span class="red"> * </span></label>
                        <input type="phone" v-model="formData.phone" placeholder="Your Phone Number" required>
                    </div>
                    <div class="contact-form">
                        <label for="shootType">Type of Shoot <span class="red"> * </span></label>  
                      <select v-model="formData.shootType" required>
                            <option value="" disabled selected>Select Shoot Type</option>
                            <option value="portraits">Portraits & Headshots</option>
                            <option value="wedding">Wedding & Events</option>
                            <option value="birthday">Birthday Shoots</option>
                            <option value="child">Child Photography</option>
                            <option value="corporate">Corporate Events</option>
                            <option value="fashion">Fashion Photography</option>
                            <option value="outdoor">Outdoor Shoots</option>
                            <option value="product">Product Photography</option>
                            <!-- <option v-for="type in shootTypes" :key="type" :value="type">{{ type }}</option> -->
                      </select>
                    </div>
                    <div class="contact-form">
                        <label for="shootDate">Proposed Date of Shoot<span class="red"> * </span></label>
                        <input type="date" v-model="formData.shootDate" required>
                    </div>    
                    <div class="contact-form">
                        <label for="shootDate">How did you hear about us? (include referral if you have one)<span class="red"> * </span></label>
                        <select v-model="formData.referral" required>
                            <option value="google">Google Search</option>
                            <option value="family">Friend/Family Referral </option>
                            <option value="event">Photography Event </option>
                            <option value="other">Others</option>
                            <!-- <option v-for="option in referralOptions" :key="option" :value="option">{{ option }}</option> -->
                        </select>   
                        <!-- <input v-if="selectedReferral === 'Other'" type="text" v-model="formData.otherReferral" placeholder="Please specify" required> -->
                    </div>
                    <div class="contact-form">
                        <label for="message">Message<span class="red"> * </span></label>
                        <textarea v-model="formData.message" placeholder="Your Message" required></textarea>
                    </div>
                    <!-- <button type="submit">
                        Send Message
                    </button> -->
                    <button type="submit" :disabled="isLoading">
                         {{ isLoading ? "Submitting..." : "Submit" }}
                    </button>
                    <p v-if="successMessage" class="success-message">{{ successMessage }}</p>
                    <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
                  </form>
                </div>
                <div class="contact-us-icons" >
                     <div>
                        <div class ="contact-us-svg">
                            <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24"><path fill="#fff" d="M20.891 2.006L20.997 2l.13.008l.09.016l.123.035l.107.046l.1.057l.09.067l.082.075l.052.059l.082.116l.052.096q.07.15.09.316l.005.106q0 .113-.024.22l-.035.123l-6.532 18.077A1.55 1.55 0 0 1 14 22.32a1.55 1.55 0 0 1-1.329-.747l-.065-.127l-3.352-6.702l-6.67-3.336a1.55 1.55 0 0 1-.898-1.259L1.68 10c0-.56.301-1.072.841-1.37l.14-.07l18.017-6.506l.106-.03l.108-.018z"/>
                            </svg>
                            <p>Danbury Crescent, South Ockendon. RM15 5XF Essex Uk</p>
                        </div>
                        <div class ="contact-us-svg">
                            <svg xmlns="http://www.w3.org/2000/svg" width="18px" height="18px" viewBox="0 0 32 32"><path fill="#fff" d="M10.25 2A3.25 3.25 0 0 0 7 5.25v21.5A3.25 3.25 0 0 0 10.25 30h11.5A3.25 3.25 0 0 0 25 26.75V5.25A3.25 3.25 0 0 0 21.75 2zM14 24h4a1 1 0 1 1 0 2h-4a1 1 0 1 1 0-2"/>
                            </svg>
                            <p>+44 7507 971045</p>
                        </div>
                        <!-- <div class ="contact-us-svg">
                            <svg xmlns="http://www.w3.org/2000/svg" width="18px" height="18px" viewBox="0 0 24 24"><path fill="#fff" d="M22 4H2v16h20zm-2 4l-8 5l-8-5V6l8 5l8-5z"/>
                            </svg>
                            <p>info@spacstudios.co.uk</p>
                        </div> -->
                     </div>
                     <div class="contact-page-map">
                        <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d974.2128380875566!2d0.2846544288050937!3d51.50584081119247!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47d8b7525c0642ad%3A0xd5dbb89871591993!2sDanbury%20Cres%2C%20South%20Ockendon%2C%20UK!5e0!3m2!1sen!2sng!4v1742444094437!5m2!1sen!2sng" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
                    </div>
                </div>                
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
