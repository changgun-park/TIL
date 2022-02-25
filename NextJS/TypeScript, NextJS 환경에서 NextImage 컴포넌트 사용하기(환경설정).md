#### TypeScript, NextJS 환경에서 Next/Image 컴포넌트 사용하기(환경설정)

---



1. CNA에 타입스크립트 옵션을 주어 프로젝트 생성

   ```
   npx create-next-app --ts
   ```

2. 수정할 파일 알아보기

   * next-env.d.ts

     ```typescript
     /// <reference types="next" />
     /// <reference types="next/image-types/global" />
     
     // NOTE: This file should not be edited
     // see https://nextjs.org/docs/basic-features/typescript for more information.
     
     ```

     ```
     A file named next-env.d.ts will be created in the root of your project. This file ensures Next.js types are picked up by the TypeScript compiler. You cannot remove it or edit it as it can change at any time.
     ```

     ```
     Instead of editing next-env.d.ts, you can include additional types by adding a new file e.g. additional.d.ts and then referencing it in the include array in your tsconfig.json.
     ```

     공식문서를 요약하자면, <strong>next-env.d.ts</strong>는 타입스크립트 컴파일러에 전달해줄 Next.js의 타입을 정의해 주는 곳이다. 

     추가적인 타입이 필요하다면, next-env.d.ts에 정의하지 말고, 새 파일을 만들고 나서 <strong>tsconfig.json</strong>이 해당 파일을 참조하도록 하는 것이 권장된다.

   * tsconfig.json

     tsconfig.json은 타입스크립트 프로젝트의 루트 디렉토리에 위치한 파일이다. 타입스크립트는 자바스크립트의 슈퍼셋이기 때문에, 반드시 자바스크립트로 컴파일해주어야 브라우저에서 작동한다. tsconfig.json은 컴파일을 할때 옵션을 명시하는 곳이다.

     ```typescript
     {
       "compilerOptions": {
         "target": "es5",
         "lib": ["dom", "dom.iterable", "esnext"],
         "allowJs": true,
         "skipLibCheck": true,
         "strict": true,
         "forceConsistentCasingInFileNames": true,
         "noEmit": true,
         "esModuleInterop": true,
         "module": "esnext",
         "moduleResolution": "node",
         "resolveJsonModule": true,
         "isolatedModules": true,
         "jsx": "preserve",
         "incremental": true
       },
       "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"],
       "exclude": ["node_modules"]
     }
     ```

   * 