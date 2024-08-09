# ckeditor
## isntall
### library 
npm install @ckeditor/ckeditor5-autoformat@41.1.0 @ckeditor/ckeditor5-basic-styles@41.1.0 @ckeditor/ckeditor5-block-quote@41.1.0 @ckeditor/ckeditor5-build-classic@41.1.0 @ckeditor/ckeditor5-ckbox@41.1.0 @ckeditor/ckeditor5-cloud-services@41.1.0 @ckeditor/ckeditor5-core@41.1.0 @ckeditor/ckeditor5-document-outline@41.1.0 @ckeditor/ckeditor5-editor-classic@41.1.0 @ckeditor/ckeditor5-essentials@41.1.0 @ckeditor/ckeditor5-heading@41.1.0 @ckeditor/ckeditor5-image@41.1.0 @ckeditor/ckeditor5-indent@41.1.0 @ckeditor/ckeditor5-link@41.1.0 @ckeditor/ckeditor5-list@41.1.0 @ckeditor/ckeditor5-media-embed@41.1.0 @ckeditor/ckeditor5-paragraph@41.1.0 @ckeditor/ckeditor5-paste-from-office@41.1.0 @ckeditor/ckeditor5-table@41.1.0 @ckeditor/ckeditor5-theme-lark@41.1.0 @ckeditor/ckeditor5-typing@41.1.0 @ckeditor/ckeditor5-ui@41.1.0 @ckeditor/ckeditor5-undo@41.1.0 @ckeditor/ckeditor5-upload@41.1.0 @ckeditor/ckeditor5-vue@5.1.0 @ckeditor/vite-plugin-ckeditor5@0.1.3
##install this library 
vite-svg-loader
##nuxt config 
### import 
const larkTheme = require.resolve("@ckeditor/ckeditor5-theme-lark");
import svgLoader from "vite-svg-loader";
import ckeditor5 from "@ckeditor/vite-plugin-ckeditor5";

### setup
vite: {
 
      plugins: [
        ckeditor5({
          theme: larkTheme,
        }),
        svgLoader(),
      ],
  },

  
