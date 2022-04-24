<template>
  <div style="width: 80%; margin-left: auto; margin-right: auto; margin-bottom: 4rem;">
    <h2>
      Terms of Use
    </h2>

    <p>
    By using this website, you agree to the terms set forth in these Terms of Use (the “Terms”) and in the <a @click="showPrivacyPolicyModal()" style="cursor: pointer; text-decoration: underline;">Privacy Policy</a> (the “Privacy Policy”).
    </p>

    <p>
    Playwaddle.com (“Waddle,” “we,” and “us”) operates the website available at  www.playwaddle.com (the “Site”), which provides the Waddle game and related features and services (the “Service”).
    </p>

    <h2>
    Terms
    </h2>

    <p>
    By accessing the Site, you are agreeing to be bound by these Terms and agree that you are responsible for the agreement with any applicable law. If you disagree with any of these Terms, you are prohibited from accessing the Site. The materials contained in this Site are protected by copyright, trademark, and other laws of the United States and foreign countries.
    </p>

    <h2>
    Prohibitions
    </h2>

    <p>
    Under your use of the Site, you may not:
    </p>

    <p>
    Attempt to reverse engineer any software contained on the Site;
    </p>
    perform any illegal activities;
    <p>
    submit or upload any illegal materials of any kind;
    </p>
    <p>
    submit or upload any profanity, hateful speech, nudity, bullying, or illicit content of any kind;
    </p>
    <p>
    submit or upload any copyright-protected materials of any kind;
    </p>
    <p>
    submit or upload any personally identifiable information of any kind to which you have not obtained consent and permission; or
    </p>
    <p>
    utilize user generated content for any illegal or malicious intent.
    </p>

    <p>
    Breaking these rules or doing anything else that we deem unfit for use of the Service will allow us to terminate your access to the Service.  We hold the right to block the access, remove the content, or delete the accounts, of anyone, for any reason whatsoever.
    </p>

    <h2>
    Disclaimer
    </h2>

    <p>
    All the materials on the Site are provided “as is”. We make no warranties, may they be expressed or implied, and this therefore negates all other warranties. Furthermore, we do not make any representations concerning the accuracy or reliability of the use of the materials on the Site or otherwise relating to such materials or any sites linked to the Site. Although we strive to provide the best experience for all users, the materials appearing on this Site may include technical, typographical, or photographic errors. We will not promise that any of the materials in the Site are accurate, complete, or current. We may change the materials contained on the Site at any time without notice.
    </p>

    <h2>
    Your Content
    </h2>

    <p>
    Some areas of the Service allow you to post or upload content and information. You retain all right, title and interest in and to your own data in the form provided to us. Subject to these Terms, you also grant to us a non-exclusive, worldwide, royalty-free right to collect, use, copy, store, transmit, modify, and create derivative works of your content in order to provide the Service to you and for any other needs deemed necessary by us to improve the Service. Although you retain ownership of your content, you also understand that publishing your content on the Service is not a substitute for registering it with the U.S. Copyright Office or any other rights organization. In addition, Waddle may monitor your use of the Service and use data and information related to such usage in an aggregate and anonymous manner, including to compile statistical and performance information related to the provision and operation of the Service (“Aggregate Data”). As between Waddle and you, all right, title and interest in the Aggregate Data and all intellectual property rights therein, belong to and are retained solely by Waddle, and Waddle may make such Aggregate Data publicly available, and use such information to the extent and in the manner it deems fit including without limitation, as required by applicable law or regulation and for purposes of data gathering, analysis, service enhancement, service improvement, and marketing, provided that no such Aggregate Data identifies you.
    </p>

    <h2>
    Feedback
    </h2>

    <p>
    We welcome feedback, comments and suggestions for improvements to the Service (“Feedback”). You can submit Feedback by emailing us at info@playwaddle.com.You grant to us a non-exclusive, transferable, worldwide, perpetual, irrevocable, fully-paid, royalty-free license, with the right to sublicense, under any and all intellectual property rights that you own or control to use, copy, modify, create derivative works based upon and otherwise exploit the Feedback for any purpose.
    </p>

    <h2>
    Liability and Indemnification
    </h2>

    <p>
    We or our suppliers will not be held responsible for any damages that could or would arise with the use or inability to use the materials on the Site, even if we or an authorized representative has been notified, orally or written, of the possibility of such damage.  For no reason whatsoever can we be held responsible for any damages relating to or pertaining to your use of the Site.
    </p>

    <p>
    To the fullest extent permitted by law, you shall defend, indemnify and hold harmless us and all of our personnel, from and against all claims, suits, proceedings, losses, liabilities, and expenses, whether in tort, contract, or otherwise, that arise out of or relate, including but not limited to attorneys’ fees and lost revenues, in whole or in part arising out of or attributable to any breach of these Terms or any activity by you in relation to your use of the Service.
    </p>

    <h2>
    Force Majeure
    </h2>

    <p>
    Any computer system, service, or electronic device, whether it is yours, a service provider’s, a network operator’s, or ours, can experience unanticipated outages, slowdowns, or capacity limitations. As a result of high internet traffic volume, transmission problems, systems capacity limitations, and any other problems, you may experience difficulty accessing the Service or communicating with us through the internet or other electronic and wireless services. The Service may be unavailable during system maintenance, for security precautions, or when interrupted by circumstances beyond our control. We will not be liable for any delay or failure to perform any obligation herein if the delay or failure is due to any of the foregoing or for any other unforeseen events that are beyond our reasonable control, such as strikes, blockade, war, terrorism, riots, natural disasters, epidemic, censorship, de-platforming, or governmental action.
    </p>

    <h2>
    Links
    </h2>

    <p>
    We have not reviewed all of the sites linked to on the Site and are not responsible for the contents of any such linked site. The presence of any link does not imply endorsement by us of the site linked to. The use of any linked website is at the user’s own risk.
    </p>

    <h2>
    Governing Law
    </h2>

    <p>
    These Terms and any action related thereto will be governed by the laws of the State of California, without regard to its conflict of laws provisions. The exclusive jurisdiction for all disputes related to these Terms and the Services will be the state and federal courts located in the Northern District of California, and you hereby waive any objection to jurisdiction and venue in such courts.
    </p>

    <h2>
    Terms Modifications
    </h2>

    <p>
    These Terms may be updated at any time.  Updates to these terms will be posted to this page, and we will notify you via email or by other means of any material changes. By continuing to use the Site after any such updates, you are agreeing to be bound by the then-current version of these Terms.
    </p>

    <h2>
    Privacy Policy
    </h2>

    <p>
    If you have questions about these Terms, the Privacy Policy, or the Services, please contact us at info@playwaddle.com.
    </p>
  
    <button @click="returnToGame()" class="button-43" role="button">Return To Game</button>
  </div>
</template>

<script>
export default {
  name: "TermsAndConditions",
  methods: {
    showPrivacyPolicyModal() {
      this.$emit("privacyPolicyClicked")
    },
    returnToGame() {
      this.$emit('returnToGame')
    },
  }
}
</script>