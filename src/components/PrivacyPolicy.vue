<template>
  <div style="width: 80%; margin-left: auto; margin-right: auto; margin-bottom: 4rem;">
  <h1>Privacy Policy</h1>

  <p>
  By using this website, you agree to the terms set forth in the  <a @click="showTermsOfUseModal()" style="cursor: pointer; text-decoration: underline;">Terms of Use</a> (the “Terms”) and in this Privacy Policy (the “Privacy Policy”).
  </p>

  <p>
Playwaddle.com (“Waddle,” “we,” and “us”) operates the website available at  www.playwaddle.com (the “Site”), which provides the Waddle game and related features and services (the “Service”).
  </p>

  <p>
  The term “Personal Information” shall have the meaning assigned to the terms “personal data” and/or “personal information” under applicable data protection laws. This Privacy Policy is used to inform Site visitors regarding our policies regarding the collection, use, and disclosure of Personal Information when visitors to the Site use our Service.
  </p>

  <p>
  If you choose to use our Service, then you agree to the collection and use of information in relation with this policy. The Personal Information that we collect is used for providing and improving the Service. We will not use or share your information with anyone except as described in this Privacy Policy.
  </p>

  <p>
  The capitalized terms used in this Privacy Policy have the same meanings as in the Terms, unless otherwise defined in this Privacy Policy.
  </p>

  <h2>
  Information Collection and Use
  </h2>

  <p>
  For a better experience while using our Service, we may require you to provide us with certain Personal Information, including but not limited to your email address and other contact information. The information that we collect will be used to contact or identify you, and help make the Service a better experience for users.
  </p>

  <p>
  If you arrive at the Site from an external source, we may record the referral data and information that referred you to us in order to learn how to better serve you and other users.
  </p>

  <p>
  We retain the Personal Information we receive as described in this Privacy Policy for as long as you use our Service or as necessary to fulfill the purpose(s) for which it was collected, provide our Service, pursue legitimate business purposes, and comply with applicable laws.
  </p>

  <h2>
  Log Data
  </h2>

  <p>
  We want to inform you that when you visit our Site, we may collect information that your browser sends to us related to your use of the Site (“Log Data”). This Log Data may include information such as your computer’s IP address, browser version, pages of the Site that you visit, the time and date of your visit, the time spent on those pages, and other statistics.  This helps us provide a better overall service for you and all users.
  </p>

  <h2>
  Cookies
  </h2>

  <p>
  Cookies are files with small amount of data that is commonly used as an anonymous unique identifier. These are sent to your browser from the website that you visit and are stored on your computer’s hard drive.
  </p>

  <p>
  Our Site uses these “cookies” to improve our Service for many reasons, including, but not limited to, helping keep track of your statistical record and performance on the Service. You have the option to either accept or refuse these cookies, and know when a cookie is being sent to your computer. If you choose to refuse our cookies, you may not be able to use some portions of our Service.
  </p>

  <h2>
  Service Providers
  </h2>

  <p>
  We may employ third-party vendors due to the following reasons:
  </p>

  <p>
  To facilitate our Service;
  To provide the Service on our behalf;
  To perform Service-related services; or
  To assist us in analyzing how our Service is used.
  </p>

  <p>
  We want to inform our users that these third parties may have access to your Personal Information in order to perform the tasks we assign to them. However, they are obligated not to disclose or use such Personal Information for any other purpose.
  </p>

  <h2>
  Security
  </h2>
  <p>
  We value your trust in providing us your Personal Information, thus we use commercially reasonable means of protecting it.  We are committed to protecting the security of your personal information and, therefore, utilize a variety of industry-grade technologies to help protect your Personal Information from unauthorized access, use, or disclosure. Remember that no method of transmission over the internet, or method of electronic storage is 100% secure and reliable, and we cannot fully eliminate all security risks associated with guaranteeing its absolute security.
  </p>
  <h2>
  Links to Other Sites
  </h2>
  <p>
  Our Service may contain links to other sites. If you click on a third-party link, you will be directed to that site. Note that these external sites are not operated by us. Therefore, we strongly advise you to review the privacy policies of such websites. We have no control over, and assume no responsibility for the content, privacy policies, or practices of any third-party sites or services.
  </p>

  <h2>
  Children’s Privacy
  </h2>

  <p>
  The Service is not directed to children under 13 years of age, and Waddle does not knowingly collect Personally Identifiable Information from children under 13 years of age. If we learn that we have collected any Personal Information from children under 13, we will promptly take steps to delete such information.
  </p>

  <h2>
  California Privacy Rights
  </h2>

  <p>
  For purposes of the California Consumer Privacy Act of 2018 (“CCPA”), we do not sell your Personal Information.
  </p>

  <p>
  In accordance with applicable law, you may have the right to: (i) request confirmation of whether we are processing your Personal Information; (ii) obtain access to or a copy of your Personal Information; (iii) receive an electronic copy of Personal Information that you have provided to us, or ask us to send that information to another company (the “right of data portability”); (iv) restrict our uses of your Personal Information; (v) seek correction or amendment of inaccurate, untrue, incomplete, or improperly processed Personal Information; and (vi) request erasure of Personal Information held about you by Waddle, subject to certain exceptions prescribed by law. If you would like to exercise any of these rights, please contact us at info@playwaddle.com. We will process such requests in accordance with applicable laws. To protect your privacy, we will take steps to verify your identity before fulfilling your request.
  </p>

  <h2>
  International Users
  </h2>

  <p>
  By using the Services, Waddle will transfer data to the United States. By choosing to visit the Site, utilize the Services or otherwise provide information to us, you agree that any dispute over privacy or the terms contained in this Privacy Policy will be governed by the laws of the State of California and the adjudication of any disputes arising in connection with Waddle or the Services will be in accordance with the Terms.
  </p>

  <p>
  If you are visiting from the European Union or other regions with laws governing data collection and use, please note that you are agreeing to the transfer of your information to the United States and to the processing of your data globally.
  </p>

  <h2>
  Changes to This Privacy Policy
  </h2>

  <p>
  We may update our Privacy Policy from time to time. Updates to these terms will be posted to this page, and we will notify you via email or by other means of any material changes. By continuing to use the Site after any such updates, you are agreeing to be bound by the then-current version of this Privacy Policy.
  </p>

  <button @click="returnToGame()" class="button-43" role="button">Return To Game</button>
  </div>
</template>

<script>

export default {
  name: "PrivacyPolicy",
  methods: {
    returnToGame() {
      this.$emit('returnToGame')
    },
    showTermsOfUseModal() {
      this.$emit("termsClicked")
    }
  }
}
</script>
