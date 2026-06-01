[Prompt]:
  Project-description: Want to create a "product-explorer", It contains product-list: Will be in endless-pagination, searchable, filterable with drawer., product-details: Will show details like - title, description, images etc in drawer.. Note: Do not use external/separate pages or routes for anything.
  Tech-stack: Vite, Vue-Typescript, Tailwindcss.
  Project-Structure: Everything will be inside src folder.
  UI/UX: 
  1- It should be production grade.
  2- Responsive in all devices.
  3- Should have light/dark mode option.
  4- Should look rich and user-friendly.

 
  Code-Rules:
  Types: shared/types/index.ts 

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
            type: string,  //eg-> sample
            data: {
                data: any;
                theme?: 'light' | 'dark',
                foo?: {
                    txt?: string, //eg=> Made with ❤️ using TypeScript & Tailwind CSS
                }
            };
        }
    },
  };
  type _$cb_TYP = {
    change: (v:{$p:_$p_TYP}) => any,
    add: (v:{/*$p:$p_TYP,*/$d:$p_TYP[data][curr][data],el:HTMLElement}) => any,
  };
  export type {p_TYP,$p_TYP,_$cb_TYP};
  
  Main: index.vue Use the below code pattern as reference, In HTML code add attribute called data-ce='[ {"k":"t-light-class","v":"class1 class2 ..."}, {"k":"t-dark-class","v":"class1 class2 ..."}  ]' on each html element which will contains theme specific classes.
  `
  <template>
    <Text />
    <div :class="${_p.f.name(`text)} text-white`"
        data-ce='[{"k":"t-light-class","v":"text-gray-900"},{"k":"t-dark-class","v":"text-white"}]'>
        {{ _$p.data.curr.data.data }}
    </div>
</template>
<script lang="ts" setup>
import type { _p_TYP, _$cb_TYP, _$p_TYP } from "../shared/types";
import Text from './src/text.vue';

const {_p, _$p, _$cb} = defineProps<{
    _p:_p_TYP,
    $p:$p_TYP,
    $cb:$cb_TYP,
}>();

const rootE = document.getElementById(_p.f.name(vue-root)) as HTMLElement;
// console.log("Root Element:", rootE);

    // Theme toggle handler
    const handleThemeToggle = () => {
        const currentTheme = _$p.data.curr.data.theme || 'light';
        const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
        
        (async() => {
            try {
                await _p.f.set_theme({name: newTheme, el_id: rootE.id});
                _$p.data.curr.data.theme = newTheme;
                document.documentElement.setAttribute('data-theme', newTheme);
            } catch (err) {
                console.error('Theme toggle failed:', err);
            }
        })();
    };

    handleThemeToggle();

</script>

<style scoped>
</style>

  `