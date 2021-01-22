<template>
  <div id="workspace" class="slds-card">
    <div class="slds-card__header slds-grid">
      <header class="slds-media slds-media_center slds-has-flexi-truncate">
        <div class="slds-media__body">
          <h2>
            <a
              href="javascript:void(0);"
              class="slds-card__header-link slds-truncate"
              title="[object Object]"
            >
              <span class="slds-text-heading_small">headline</span>
            </a>
          </h2>
        </div>
      </header>
    </div>
    <div class="slds-card__body slds-card__body_inner">
      <div class="slds-form-element">
        <label class="slds-form-element__label" for="text-input-id-1"
          >headline text</label
        >
        <div class="slds-form-element__control">
          <input
            id="text-input-id-1"
            type="text"
            ref="text"
            class="slds-input"
            v-model="textInput"
            @change="getContent"
            @input="getContent"
            value=""
            placeholder="Find your ideal hotel"
          />
        </div>
      </div>
    </div>
    <br />
    <hr />
    <br />
    <div>
      {{ this.mjmloutput }}
    </div>
    <br />
  
  </div>
</template>
<script>
import BlockSDK from "blocksdk";
// import MJML from "mjml";
// const mjml2html = require('mjml')
// import { createRenderer } from "vue-server-renderer";

export default {
  data() {
    return {
      content: "",
      mjmloutput: null,
      textInput: "Find your ideal hotel",
    };
  },
  methods: {
    generateContent() {
      var style =
        '<style type="text/css">\
      /* Global Rules */\
      td.font20 { font-size: 20px !important; line-height: 100% !important; }\
      td.minheight, div.minheight { font-size: 1px !important; line-height: 1px !important; mso-line-height-rule: exactly; }\
      td.font24-elh { font-size: 24px !important; line-height: 30px !important; mso-line-height-rule: exactly; }\
      /* Mobile Rules */\
      @media only screen and (max-width:480px) {\
      body, .bg { background: #ffffff !important; }\
      .resimg { width: 100% !important; min-width: 100% !important; height: auto !important; }\
      .mobfullw { width: 100% !important; min-width: 0 !important; }\
      .searchbar { padding-left: 16px !important; padding-top: 16px !important; padding-right: 16px !important; padding-bottom: 16px !important; }\
      }\
      </style>';
      var bodycontent =
        '<!-- Begin headline -->\
      <table border="0" cellpadding="0" cellspacing="0" width="700" align="center" class="mobfullw" style="margin: 0 0 0 0;min-width: 300px;border-collapse: collapse;font-family: arial, sans-serif;">\
          <tbody><tr>\
          <td align="center" style="padding-top: 24px; color: #37454d;font-size: 16px !important;line-height: 115% !important;">\
              <table border="0" cellpadding="0" cellspacing="0" width="588" align="center" class="mobfullw" style="margin: 0 0 0 0;min-width: 300px;border-collapse: collapse;font-family: arial, sans-serif;">\
              <tbody><tr>\
                  <td width="100%" class="minheight" style="padding: 0 16px 0 16px;color: #37454d;mso-line-height-rule: exactly;font-size: 1px !important;line-height: 1px !important;">\
                  <table border="0" cellpadding="0" cellspacing="0" width="100%" align="center" class="mobfullw" style="margin: 0px; min-width: 300px; border-collapse: collapse; font-family: arial, sans-serif;">\
                      <tbody><tr>\
                      <td class="font24-elh" align="left" style="padding: 0 0 16px 0;color: #37454d;font-size: 24px !important; line-height: 30px !important; mso-line-height-rule:exactly;">\
                          <b class="trv_amppreview">' +
        this.textInput +
        "</b>\
                      </td>\
                      </tr>\
                  </tbody></table>\
                  </td>\
              </tr>\
              </tbody></table>\
          </td>\
          </tr>\
      </tbody></table>\
      <!-- End headline -->";


    const mjml2html = require("mjml-web");

    // registerComponent(MyComponent)
    const mjmloutputhtml = mjml2html(`
  <mjml>
    <mj-body>
      <mj-section>
        <mj-column>
          <mj-text>
            Hello World!
          </mj-text>
        </mj-column>
      </mj-section>
    </mj-body>
  </mjml>
`);
    console.log(mjmloutputhtml);
    this.mjmloutput = mjmloutputhtml.html;


      this.content = style.concat(bodycontent);
      // this.content = mjmloutputhtml;
      return this.content;
    },
    getContent() {
      /**
       * Generates the content block and set the datas on users input
       */
      // var sdk = new BlockSDK(['blocktester.herokuapp.com', 'localhost', 'marketingcloudapps.com', "https://nuxt-mjml-sfblock.netlify.app/", "https://nuxt-mjml-sfblock.netlify.app/trv-logo-header-v2/"], true);
      var sdk = new BlockSDK();
      sdk.getData( gata => {
        console.log("Getcontent funtiion get data: ",gata);
      } );
      sdk.setData({
        textInput: this.textInput,
      });
      sdk.setContent(this.generateContent());
    },
  },
  mounted() {
    var sdk = new BlockSDK();
    var self = this;
    sdk.getData(function (data) {
      console.log("Mounted get data: ",data);
      if (data.textInput !== undefined) {
        self.textInput = data.textInput;
        self.$refs["text"] = self.textInput;
      }
      sdk.setContent(self.generateContent());
    });

//     const { default: mjml2html, registerComponent } = require("mjml-web");

//     // registerComponent(MyComponent)
//     const mjmloutputhtml = mjml2html(`<mjml>
//   <mjml-body>
//     <mj-section>
//       <mj-column>
//           <mj-text font-size="20px" color="#F45E43" font-family="helvetica">Hello {{ name }}</mj-text>
//       </mj-column>
//     </mj-section>
//   </mjml-body>
// </mjml>`).html;
//     console.log(mjmloutputhtml);
//     this.mjmloutput = mjmloutputhtml;
  },
};
</script>


<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
}
</style>