
# [A.I-Based-Dev]..
  [Prompt]:
  Project-description: Want to create a "sign in".
  Tech-stack: Vite, Vanilla-Typescript, Tailwindcss.
  Project-Structure: Everything will be inside `src` folder and outside `src` folder, provide `index.ts` with all usage means we should be able to run app via `index.ts`.
  UI/UX: 
  1- It should be production grade.
  2- Responsive in all devices.
  3- Should have light/dark mode option.
  4- Should look rich and user-friendly.

 
  Code-Rules:
  Types: `_$cb_TYP` please do not use callbacks or anything to re-render `Renderer` and `Hydrator`.. Instead if something changes in `Renderer`
  then you listen it in `Hydrator` for-example => `document.getElementById(ID).click=>{};`.
  `
  type _p_TYP = {
    f:{
        name:(v:string)=>string,
        get_lib:(v:{name:string,run_from:any})=> any,
        set_theme:(v:{name:string,el_id:string})=> any,
        path:(v:string)=>string,
    }
  };
  type _$p_TYP = {
    data: {
        curr: {
            "id": string,
            type: "sign_in",
            data: {
                data: any;
                theme?: 'light' | 'dark',
                foo?: {
                    txt?: string, //eg=> `Made with ❤️ using TypeScript & Tailwind CSS`
                }
            };
        }
    },
  };
  type _$cb_TYP = {
    change: (_v:{_$p:_$p_TYP}) => any,
    add: (_v:{/*_$p:_$p_TYP,*/$d:_$p_TYP[`data`][`curr`][`data`],el:HTMLElement}) => any,
  };
  export type {_p_TYP,_$p_TYP,_$cb_TYP};
  
  `
  Renderer: Use the below code pattern as reference, and you can use `_$r.r` for putting `HTML` code with attribute called `data-ce='[ {"k":"t-light-class","v":"class1 class2 ..."}, {"k":"t-dark-class","v":"class1 class2 ..."}  ]'` on each `html` element which will contains theme specific classes.
  and `_$r.style` for putting `CSS` code.
  It is a SSR-First pattern and does not support any post-processing of `typescript` logic/function. for-example => `document.getElementById("my_id").click => {};`
  Also, make it only one-time runnable no `re-render` is allowed.
  `
  import type { _p_TYP, _$cb_TYP, _$p_TYP } from "../shared/types";
  import  "../style.css";
  const index = async (_p:_p_TYP) => {
    return {
        set: async (_$p:_$p_TYP,_$cb?:_$cb_TYP) => {  
            console.log(`--renderer [${_$p[`data`][`curr`].type}]`);
            const _$u = {
                value: (): string => {
                    return _$p[`data`][`curr`].data[`data`];
                },
            };
            const _$r = {
                r: (() => {
                let _n = `
                <div id="${_p.f.name(`root`)}"   >

                  <div class="${_p.f.name(`text`)} text-white" 
                  data-ce='[{"k":"t-light-class","v":"text-gray-900"},{"k":"t-dark-class","v":"text-white"}]'
                  >
                  ${_$u.value()}
                  </div>


                  <!-- Footer -->
                  <footer
                    class="mt-16 mb-2 text-center text-gray-500"
                    data-ce='[{"k":"t-light-class","v":"text-gray-500"}, {"k":"t-dark-class","v":"text-gray-400"}]'
                  >
                    <!--p>Made with ❤️ using TypeScript & Tailwind CSS</p-->
                    <p>${_$p.data.curr.data?.foo?.txt || ``}</p>
                  </footer>

                </div>
                `;
                return _n;
                })(),
                head: (() => {
                let _n = `
                <title></title>
                <meta name="description" content="">
                <script type="application/ld+json">
                {
                  "@context": "https://schema.org",
                  "@type": "",
                  "name": ""
                }
                </script>
                `;
                return _n;
                })(),
                style: (()=>{
                let _n = ``;
                _n = `
                

                .${_p.f.name(`text`)} {
                   background: transparent;
                }
                `;
                return _n;
                })(),

            };
            return _$r;
        },
    };
  }
  export {index, index as renderer}
  `
  Hydrator: Use the below code pattern as reference, and you can use `(async(mE) => {})(mE);` for putting `Typescript` and `DOM` code.
  Also, make it only one-time runnable no `re-hydration` is allowed.
  `
  import type { _p_TYP, _$cb_TYP, _$p_TYP } from "../shared/types";
  const index = async (_p:_p_TYP) => {
    return {
        set: async (_$p:_$p_TYP,_$cb?:_$cb_TYP) => {
            /*const _$p = createObserver(_$p_, (path, key, oldVal, newVal) => {_$cb?.change({_$p:_$p_})});*/ //not supported in some browsers..
            console.log(`--hydrator [${_$p[`data`][`curr`].type}]`);
            const _$u = {
            };
            const _$r = {
                r: (()=>{
                let _n = ``;
                return _n;
                })(),
                style: (() => {
                let _n = ``;
                /*_n = `
                .${_p.f.name(`text`)} {
                   background: #cccccc;
                }
                `;*/
                return _n;
                })(),
                //set..
                evt: {
                    change: () => {
                        _$cb?.change({_$p:_$p});
                    }
                }
            };
            const rootE = document.getElementById(_p.f.name(`root`)) as HTMLElement;
            /*rootE!.onclick = () => {
                alert(`--root`);
            };*/
            (async(mE) => {
            /* Our `Typescript` and `DOM` code */

                // Toggle theme
                const handleThemeToggle = () => {
                    //set vars..
                    const currentTheme = _$p.data.curr.data.theme;
                    const newTheme = ((v)=>{
                    if (v==`dark`) {
                        return `light`;
                    }
                    if (v==`light`) {
                        return `dark`;
                    }
                    return v;
                    })(currentTheme);


                    //set..
                    (async()=>{
                    try {
                    await _p.f.set_theme({name:`${newTheme}`,el_id:`${rootE.id}`});
                    //all ok..
                    // Update data
                    _$p.data.curr.data.theme = newTheme;
                    } catch (err) {}
                    })();

                    //set..
                    //console.log(`newTheme: ${newTheme}`);


                };

            //set..
            _$cb?.add({$d:_$p[`data`].curr[`data`],el:mE!});
            })(rootE);
            return _$r;
        },
    };
  }
  export {index, index as hydrator}
  `
  

