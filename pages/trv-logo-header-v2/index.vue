<template>
  <div class="container">
    <div style="margin: 20px">
      <h2>trv-logo-header-v2</h2>
      <br />

      <nuxt-link to="/"><button>Home</button></nuxt-link><br />
    </div>
    <div style="margin: 20px">
      <label for="select-01">Select Logo</label>
      <div>
        <select
          id="select-01"
          @change="getContent()"
          v-model="inputLogoUrl"
          ref="logo-list"
        >
          <option value="">please select</option>
          <option
            value="https://imgma.trivago.com/image/upload/v1562670228/Assets/newsletter/header/logo_color_2x.png"
          >
            logo_color_2x.png
          </option>
          <option
            value="https://imgma.trivago.com/image/upload/v1562670228/Assets/newsletter/header/trivago_magazine_logo_2x.png"
          >
            trivago_magazine_logo_2x.png
          </option>
          <option
            value="https://imgma.trivago.com/image/upload/v1562670228/Assets/newsletter/header/thm_logo_532x64.png"
          >
            thm_logo_532x64.png
          </option>
          <option
            value="https://imgma.trivago.com/image/upload/v1562670228/Assets/newsletter/header/trivago-logo-thm_2x.png"
          >
            trivago-logo-thm_2x.png
          </option>
          <option
            value="https://imgma.trivago.com/image/upload/v1562670228/Assets/newsletter/header/trv-bstudio_emailhead_Adj2_2x.png"
          >
            trv-bstudio_emailhead_Adj2_2x.png
          </option>
        </select>
      </div>
      <div style="margin-top:20px;">
        <label for="input-url">url header</label>
        <div>
          <input
            style="width:200px;"
            type="text"
            id="input-url"
            ref="url"
            v-model="inputExitURL"
            @change="getContent"
            @input="getContent"
            value=""
            placeholder="https://www.trivago.com"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import BlockSDK from "blocksdk";
export default {
  // template: `
  //     <mjml>
  //     <mjml-body>
  //         <mj-section>
  //         <mj-column>
  //             <mj-text font-size="20px" color="#F45E43" font-family="helvetica">Hello This is Header Logo V2</mj-text>
  //         </mj-column>
  //         </mj-section>
  //     </mjml-body>
  //     </mjml>`,
  data() {
    return {
      content: "",
      inputLogoUrl:
        "https://imgma.trivago.com/image/upload/v1562670228/Assets/newsletter/header/logo_color_2x.png",
      inputExitURL: "https://www.trivago.com",
      checkboxCip: false,
      inputCIP: "",
      inputCIPTC: "",
    };
  },
  methods: {
    generateContent() {
      var concrateURL = this.inputExitURL;
      if (this.checkboxCip) {
        concrateURL += "&cip=" + this.inputCIP + "&cip_tc=" + this.inputCIPTC;
      }
      var style =
        '<style type="text/css">#outlook a { padding:0; } body { margin:0;padding:0;-webkit-text-size-adjust:100%;-ms-text-size-adjust:100%; } table, td { border-collapse:collapse;mso-table-lspace:0pt;mso-table-rspace:0pt; } img { border:0;height:auto;line-height:100%; outline:none; text-decoration:none;-ms-interpolation-mode:bicubic; } p { display:block;margin:13px 0; }</style><!--[if mso]>   <xml>  <o:OfficeDocumentSettings> <o:AllowPNG/>  <o:PixelsPerInch>96</o:PixelsPerInch>  </o:OfficeDocumentSettings> </xml> <![endif]--><!--[if lte mso 11]>  <style type="text/css"> .mj-outlook-group-fix { width:100% !important; } </style>  <![endif]--><style type="text/css">@media only screen and (min-width:480px) {  .mj-column-px-554 { width:554px !important; max-width: 554px; } }</style><style type="text/css">@media only screen and (max-width:480px) {table.mj-full-width-mobile { width: 100% !important; }td.mj-full-width-mobile { width: auto !important; }}</style>';

      var bodycontent =
        '<div style="background-color:#eeeeee;"><!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" style="width:600px;" width="600" ><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly;"><![endif]--><div style="background:#ffffff;background-color:#ffffff;margin:0px auto;max-width:600px;"><table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ffffff;background-color:#ffffff;width:100%;"><tbody><tr><td style="direction:ltr;font-size:0px;padding:20px 0;text-align:center;"><!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:554px;" ><![endif]--><div class="mj-column-px-554 mj-outlook-group-fix" style="font-size:0px;text-align:left;direction:ltr;display:inline-block;vertical-align:top;width:100%;"><table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top;" width="100%"><tr><td align="left" style="font-size:0px;padding:10px 25px;word-break:break-word;"><table border="0" cellpadding="0" cellspacing="0" role="presentation" style="border-collapse:collapse;border-spacing:0px;"><tbody><tr><td style="width:102px;"><a href="'+concrateURL+'" target="_blank"><img height="32" src="'+this.inputLogoUrl+'" style="border:0;display:block;outline:none;text-decoration:none;height:32px;width:100%;font-size:13px;" width="102"></a></td></tr></tbody></table></td></tr></table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></tbody></table></div><!--[if mso | IE]></td></tr></table><![endif]-->';
      this.content = style.concat(bodycontent);
      return this.content;
    },
    getContent() {
      /**
       * Generates the content block and set the datas on users input
       */
      sdk.setData({
        inputLogoUrl: this.inputLogoUrl,
        inputExitURL: this.inputExitURL,
        checkboxCip: this.checkboxCip,
        inputCIP: this.inputCIP,
        inputCIPTC: this.inputCIPTC,
      });
      sdk.setContent(this.generateContent());
    },
  },
  mounted() {
    // const sdk = new BlockSDK(["blocktester.herokuapp.com", "localhost", "marketingcloudapps.com", "https://nuxt-mjml-sfblock.netlify.app/", "https://nuxt-mjml-sfblock.netlify.app/trv-logo-header-v2/"], true);
    const sdk = new BlockSDK();
    var self = this;
    sdk.getData(function (data) {
      if (data.inputLogoUrl !== undefined) {
        self.inputLogoUrl = data.inputLogoUrl;
        self.$refs["logo-list"] = self.inputLogoUrl;

        self.inputExitURL = data.inputExitURL;
        self.$refs["url"] = self.inputLogoUrl;

        self.checkboxCip = data.checkboxCip;
        self.$refs["check-cip"] = self.checkboxCip;

        self.inputCIP = data.inputCIP;
        self.$refs["inputCIP"] = self.inputCIP;

        self.inputCIPTC = data.inputCIPTC;
        self.$refs["inputCIPTC"] = self.inputCIPTC;
      }
      sdk.setContent(self.generateContent());
    });
  },
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
}
</style>
