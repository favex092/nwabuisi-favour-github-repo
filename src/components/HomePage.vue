<template>
  <div class="home">
    <AppLayout />
    <h1>ABOUT ME</h1>
    <div className="about-container">
      <div className="about-me">
        <div className="about-me-img">
          <img src="../assets/me.jpg" alt="My profile" />
        </div>
      </div>

      <div className="about-content">
        <div className="about-cards">
          <article className="about-card">
            <h5>Experience</h5>
            <small>Over 1.5+ Years</small>
          </article>
          <article className="about-card">
            <h5>Projects</h5>
            <small>25+ Completed</small>
          </article>
        </div>
        <div class="about-desc-cont">
          <p class="about-desc">
            My one year plus of experience as a Front End Developer(student) at AltSchoolAfrica has honed my CSS3 and HTML5 skills, as well as my knowledge of mobile and responsive design. My professional experience includes bringing the wireframes of the UX designer to life through HTML5 and CSS3, as well as collaborating with Back End Developers to create a stellar finished product. I think my skills and experience makes me a great fit and
            I’m passionate about developing interactive websites and web features to drive up online traffic and sales, bringing the company to greater heights.
          </p>
        </div>

        <a href="mailto:favex2986@gmail.com" className="btn"> CONTACT ME </a>
      </div>
    </div>
  </div>
</template>

<script>
import AppLayout from "./AppLayout.vue";
export default {
  name: "HomePage",
  components: {
    AppLayout,
  },
};
</script>

<style scoped>
.home {
  background:lavender;
}
h1 {
  text-align: center;
  font-size: 2rem;
  font-weight: 600;
  margin: 2rem 0 4rem 0;
}
.about-container {
  display: grid;
  align-items: center;
  grid-template-columns: repeat(2, 1fr);
  gap: 2rem;
}
.about-me {
  width: 50%;
  height: fit-content;
  border-radius: 2rem;
  background: linear-gradient(45deg, transparent, gold, transparent);
  display: grid;
  place-items: center;
  margin-left: 10%;
}
.about-me-img {
  border-radius: 2rem;
  width: 100%;
  overflow: hidden;
  transform: rotate(-10deg);
  transition: 1s ease-in-out;
}
.about-me-img img {
  width: 100%;
  padding: 5px 1rem;
  border-radius: 3rem;
}
.about-content {
  margin: 0 1rem 2rem 1rem;
}
.about-cards {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 2rem;
  padding: 2rem 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
.about-card {
  border: 1px solid goldenrod; 
  /* #e01f1f; */
  width: 40%;
  border-radius: 1rem;
  padding: 1rem;
  text-align: center;
  transition: 0.5s ease-in-out;
}
.about-card:hover {
  transform: scale(1.05);
  cursor: default;
}
.about-card h5 {
  font-size: 1rem;
  font-weight: 600;
}
.about-card small {
  color: #6d6a6a;
  font-size: 0.8rem;
}
.about-desc-cont {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 1rem 0 0;
}
.about-desc {
  font-size: 1.2rem;
  line-height: 1.8;
  margin: 1.5rem 0 2rem 0;
  text-align: justify;
}
.btn {
  color: #6d6a6a;
  font-weight: 600;
  font-size: 18px;
  border: 1px solid  #57370D;
  /* #d85d5d; */
  width: 150px;
  border-radius: 1rem;
}
.btn:hover {
  background: #57370D;
  color: #fff;
  border: 1px solid ;
  transition: 0.5s ease-in-out;
}
@media screen and (max-width: 1024px) {
  .about-container {
    grid-template-columns: 1fr;
    gap: 0;
  }
  .about-me {
    width: 60%;
    margin: 0.1rem auto 1.5rem;
  }
  .about-me-img {
    width: 60%;
  }
}
@media screen and (max-width: 600px) {
  .about-me {
    width: 65%;
    margin: 0 auto 3rem;
  }
  .about-cards {
    grid-template-columns: 1fr 1fr;
  }
  .about-content {
    text-align: center;
  }
  .about-content p {
    margin: 1.5rem 0;
  }
  .about-me-img {
    width: 100%;
  }
}
@media screen and (max-width: 400px) {
  .about-me {
    width: 80%;
  }
  .about-cards {
    grid-template-columns: 1fr;
  }
}
</style>