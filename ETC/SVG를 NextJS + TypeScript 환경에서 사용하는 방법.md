### SVG를 NextJS 환경에서 Component로 사용하는 방법

---

[SVGR 공식 홈페이지](https://react-svgr.com/docs/next/)



1. 먼저 패키지를 설치한다.

   svgr은 svg를 리액트 컴포넌트로 사용할 수 있도록 만들어주는 패키지이다.

   ```
   npm install @svgr/webpack --save-dev
   ```

2. next.config.js 수정

   next.config.js라는 파일은 도대체 어떤 파일인가? [NextJS 공식 홈페이지](https://nextjs.org/docs/api-reference/next.config.js/introduction)

   ```typescript
   module.exports = {
     webpack(config) {
       config.module.rules.push({
         test: /\.svg$/,
         use: ["@svgr/webpack"]
       });
   
       return config;
     }
   };
   ```

   

3. typing.d.ts 에 추가

   ```typescript
   declare module "*.svg" {
     const content: any;
     export default content;
   }
   ```

   

