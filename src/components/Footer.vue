
<template>
    <footer>
       <div class="footer-first-section">
            <div class="footer-logo">
                    <img src="/images/floggo.png">
            </div>
            <div class="footer-container">
                <div class="footer-about-container">
                    <h4>ABOUT</h4>
                    <p> Spac Studios is more than just a photography brand: 
                        we are storytellers, capturing emotions, light, 
                        and artistry in their purest forms.
                        From elegant portraits to breathtaking landscapes, 
                        corporate branding to intimate celebrations, we 
                        specialize in delivering timeless visuals that leave 
                        a lasting impression.
                    </p>
                </div>
                <div class="quicklink-container">
                    <h4>QUICK LINKS</h4>
                    <ul>
                    <li>
                        <router-link to="/">Home</router-link>
                    </li>
                    <li>
                        <router-link to="/about-us">About</router-link>
                    </li>
                    <li>
                        <router-link to="/birthday-shoots">Birthday Shoot</router-link>
                    </li>
                    <li>
                        <router-link to="/gallery">Gallery</router-link>
                    </li>
                    <li>
                        <router-link to="/pricing">Pricing</router-link>
                    </li>
                    <li>
                        <router-link to="/contact">Contact & Bookings</router-link>
                    </li>
                </ul>
                </div>
                <div class="instagram-container">
                    <h4>INSTAGRAM POSTS</h4>
                    <div class="instagram-image-grid">
                        <a href= "https://www.instagram.com/spac_studios?utm_source=ig_web_button_share_sheet&igsh=ZDNlZDc0MzIxNw==" target="_blank">
                                <img src="/images/jpeg-optimizer_banner-img1.jpg" id="img1">
                        </a>     
                        <a href= "https://www.instagram.com/spac_studios?utm_source=ig_web_button_share_sheet&igsh=ZDNlZDc0MzIxNw==" target="_blank">
                                <img src="/images/jpeg-optimizer_banner-img2.jpg" >
                        </a>     
                        <a href= "https://www.instagram.com/spac_studios?utm_source=ig_web_button_share_sheet&igsh=ZDNlZDc0MzIxNw==" target="_blank">
                                <img src="/images/img38.png" id="img3">
                        </a>     
                        <a href= "https://www.instagram.com/spac_studios?utm_source=ig_web_button_share_sheet&igsh=ZDNlZDc0MzIxNw==" target="_blank">
                                <img src="/images/img25.jpg">
                        </a>     
                        <a href= "https://www.instagram.com/spac_studios?utm_source=ig_web_button_share_sheet&igsh=ZDNlZDc0MzIxNw==" target="_blank">
                                <img src="/images/img20.jpg" id="img5">
                        </a>     
                        <a href= "https://www.instagram.com/spac_studios?utm_source=ig_web_button_share_sheet&igsh=ZDNlZDc0MzIxNw==" target="_blank">
                                <img src="/images/banner-img3.jpg" id="img5">
                        </a>     
                    </div>
                </div>
            </div>
       </div>
       <div class="footer-second-section">
            <div class="copyright-container">
                <p>
                    COPYRIGHT © 2024 SPAC STUDIOS. ALL RIGHT RESERVED. POWERED BY 
                    <a href="https://wa.me/2349161038393" target="_blank" rel="noopener">
                        MAROSN INTELLIGENCE
                    </a>
                </p>
            </div>
       </div>
    </footer>
</template>


<style setup>

.footer-first-section {
    background-color: rgb(21, 21, 21);
    padding: 40px 0px 20px 0px;
}
.footer-container {
    display: flex; 
    flex-direction: row;
    justify-content: space-between;
    margin: auto;
    width: 90%;
    
}

.footer-logo {
    text-align: center;
    margin-bottom: 10px;
}

.footer-logo img {
    width: 150px;
    cursor: pointer;
}

.footer-container h4 {
    color: white;
    font-size: 16px;
    font-weight: 600;
}

.footer-about-container {
    width: 40%;
    padding-right: 50px;
}

.footer-about-container p {
    color: rgb(240, 240, 240);
    font-size: 13px;
    line-height: 24px;
}

.quicklink-container {
    width: 25%;
}

.quicklink-container a {
    color: rgb(240, 240, 240);
    display: block;
    font-size: 13px;
    line-height: 24px;
    text-decoration: none;
    text-transform: uppercase;
    cursor: pointer;
}

.quicklink-container a:hover {
    color: rgb(160, 160, 160);
   
}

.quicklink-container ul {
    margin: 0px;
    padding: 0px;
}

.quicklink-container li {
    list-style-type: none;
}

.instagram-container {
    width: 35%;
}

.instagram-image-grid {
    display: grid;
    /* grid-template-columns: repeat(3, 1fr); */
    grid-template-columns: auto auto auto;
    justify-content: flex-start;
    gap: 3px;
}

.instagram-image-grid a{
    width: 80px;           
    height: 80px;
}


.instagram-container img{
    /* width: 100%;  */
    /* height: 70px;  */
    /* object-fit: cover;
    aspect-ratio: 1 / 1; */
    width: 80px;           
    height: 80px;         
    object-fit: cover;   
    transition: 0.3s ease;
}

.instagram-container img:hover{
    filter:brightness(0.8);
    filter: grayscale(100%);
}

.footer-second-section {
    background-color: black;
    padding: 20px 0px
}

.copyright-container {
    width: 90%;
    margin: auto;
}

.copyright-container p {
    margin: 0px;
    color: rgb(210, 210, 210);
    font-size: 10px;
}

.copyright-container a {
    cursor: pointer;
    color: rgb(210, 210, 210);
    text-decoration: none;
}



/* #img1 {
    grid-column: 1 / span 2;
    
} */

@media (max-width:992px) {
   .footer-container {
        display: flex; 
        flex-direction: column;
   }

   .footer-container h4 {
       margin-bottom: 10px;
       font-size: 15px;
    }

    .footer-about-container p {
        font-size: 12px;
    }

    .quicklink-container a {
        font-size: 12px;
        line-height: 23px;
    }


   .footer-about-container {
        width: 100%;
        padding-right: 0px;
    }

   .quicklink-container {
        width: 100%;
    }

    .instagram-container {
        width: 100%;
    }

    .copyright-container p {
        font-size: 10px;
    }

}
</style>