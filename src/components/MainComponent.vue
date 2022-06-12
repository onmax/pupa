<template>
  <main class="bg-slate-700 h-screen w-screen grid place-items-center">
    <div
      v-if="status === 0"
      class="h-full w-full relative grid place-items-center"
    >
      <h1 class="font-mono text-9xl font-bold text-white">
        DOC ME
      </h1>
      <button
        class="bottom-40 bg-emerald-800 px-8 py-5 rounded-lg text-emerald-50 font-bold text-xl cursor-pointer hover:bg-emerald-900 transition absolute"
        @click="clicked"
      >
        Launch app
      </button>
    </div>
    <div
      v-else-if="status === 1"
      class="text-6xl font-bold text-white"
    >
      Joining...
    </div>
    <div
      v-else
      class="flex w-screen"
    >
      <div
        class="grid place-items-center flex-1"
        :class="{'mx-8': status >= 4}"
      >
        <div
          class="relative"
          :class="status >= 4 ? 'w-full' : 'w-3/4'"
        >
          <video
            ref="video$"
            loop
            class="rounded-lg w-full shadow-lg"
            src="/meeting.mp4"
          />
          <transition name="fade">
            <div
              v-if="status===3"
              class="bottom-0 w-full right-0 h-80 bg-gradient-to-b from-transparent to-slate-800 z-10 absolute rounded-b-lg"
            />
          </transition>
          <!-- TODO transition -->
          <div
            v-if="status===3"
            class="bg-white rounded-xl right-4 bottom-4 absolute flex flex-col px-10 py-4 shadow-2xl z-20"
          >
            <img
              class="w-40 mx-auto mb-4"
              src="/logo.jpeg"
              alt=""
            >
            <div class="flex justify-end">
              <button
                class="bg-emerald-800 p-3 shadow-sm rounded-lg text-emerald-50 font-bold text-xl cursor-pointer hover:bg-emerald-900 transition mr-6"
                @click="startDocMe"
              >
                Use now!
              </button>
              <button class="text-slate-600">
                Not now
              </button>
            </div>
          </div>
        </div>
      </div>

      <aside
        :class="{'w-[500px] h-screen bg-white px-6 py-8 overflow-auto': status >= 4, 'w-0': status < 4}"
      >
        <span v-if="status === 4">Loading...</span>
        <a
          v-if="status === 5"
          href="https://6483-119-13-68-59.eu.ngrok.io/report"
          class="bg-red-800 p-1 shadow-sm rounded-lg px-3 text-red-50 font-bold text-lg cursor-pointer hover:bg-red-900 fixed"
        >
          End meeting
        </a>
        <p
          v-if="status === 5"
          ref="p$"
          class="pp pt-12"
        />
      </aside>
    </div>
  </main>
</template>

<script setup lang="ts">
import { nextTick, Ref, ref } from '@vue/runtime-dom'

  
let status = ref(0)
let video$: Ref<null | HTMLVideoElement> = ref(null)
let p$: Ref<null | HTMLParagraphElement> = ref(null)

const content = `
  Joy: Hello everyone!
  <br/>
  Ray: Hello!
  <br/>
  Joy: So, now that everyone is here, let's start the meeting. I would like to talk about the strategy we have in place.
  <br/>
  Ray: What is the strategy?
  <br/>
  Rahul: The strategy for the next quarter is to create a new product that will be used by the entire company.
  <br/>
  Joy: What is the product?
  <br/>
  Max: <span>We are holding a hackthon event in Huawei Office located in stockholm at 2pm on 12th June</span>
  <br/>
  Rahul: What is the power?
  <br/>
  Max: The power is in the simplicity.
  <br/>
  Rudraksh: An app to track your expenses.
  <br/>
  Rahul: As we talked, last week, we would like to make it with HMS. Placerat duis ultricies lacus sed turpis. Interdum consectetur libero id faucibus nisl. Semper quis lectus nulla at volutpat diam. Justo nec ultrices dui sapien eget mi proin sed libero. Posuere ac ut consequat semper viverra nam libero justo laoreet. In nisl nisi scelerisque eu. In ante metus dictum at tempor commodo ullamcorper a. Amet tellus cras adipiscing enim eu. Molestie ac feugiat sed lectus. Enim praesent elementum facilisis leo vel fringilla est ullamcorper eget. Non curabitur gravida arcu ac.
  <br/>

Max: What is it about?
  <br/>
Joy: We need to come up with an idea solving some chanllenges relating to WFM. 
We need <span>25 participants</span> for this event and some of the employees in our office should also join as host and expertise to assist our student ambassadors to conduct this event.
When the event starts, we will provide agenda to all of the participants helping them know the time schedule as I don't want participants feel confused about what will happen.
The first day of the <span>event will last 5 hours</span> and <span>Ray will have to give a welcome speech</span>. <span>Rudrask, your job here is to give some HMS introductions</span> to our participants so that they could have a clear guidance about our product. <span>Miguel, you need to present your Game development</span>, which is mainly to give them an idea or a direction about where they could go. <span>Rajul, i need you to give a speech around topic of Health and awareness</span>. I'm sure you could definitely handle this but you need to have some more prepare for this part as this part is the most confusing part to our participants you know. <span>Max, you will need to go with our Huawei Cloud</span> section as you are from cloud department so you are the one who is familiar with cloud the most in our team. That's all of the arrangement for the event. I hope we can make it possible

  <br/>

Ray: Nibh mauris cursus mattis molestie a iaculis. Volutpat consequat mauris nunc congue nisi vitae suscipit tellus mauris. Et malesuada fames ac turpis egestas integer eget aliquet. Dignissim diam quis enim lobortis scelerisque fermentum. Ultrices sagittis orci a scelerisque purus semper eget duis. Magna eget est lorem ipsum dolor sit amet. Ac ut consequat semper viverra nam libero. Arcu ac tortor dignissim convallis aenean et tortor at risus. Proin nibh nisl condimentum id venenatis a condimentum vitae. Aliquam vestibulum morbi blandit cursus risus at ultrices. Vitae congue mauris rhoncus aenean vel elit scelerisque mauris. Blandit massa enim nec dui nunc mattis enim ut tellus. Ut pharetra sit amet aliquam id diam. Enim blandit volutpat maecenas volutpat blandit aliquam etiam erat velit. Morbi tristique senectus et netus et malesuada fames ac. Augue interdum velit euismod in pellentesque massa placerat. Turpis massa tincidunt dui ut. Aliquet sagittis id consectetur purus.
  <br/>

Rajul: Aliquam malesuada bibendum arcu vitae elementum curabitur. Quis vel eros donec ac. Nisi vitae suscipit tellus mauris a. Eu scelerisque felis imperdiet proin fermentum leo vel orci. Adipiscing enim eu turpis egestas. Augue mauris augue neque gravida in fermentum. Elit duis tristique sollicitudin nibh sit amet commodo. Maecenas accumsan lacus vel facilisis volutpat est velit. Accumsan lacus vel facilisis volutpat. Morbi tincidunt augue interdum velit. Porttitor leo a diam sollicitudin tempor id eu.
  <br/>

Max: Urna nec tincidunt praesent semper feugiat. Sed risus ultricies tristique nulla. Ut ornare lectus sit amet. Et pharetra pharetra massa massa ultricies mi quis. Venenatis a condimentum vitae sapien pellentesque habitant morbi. Purus in mollis nunc sed id. Vitae sapien pellentesque habitant morbi. Nullam eget felis eget nunc. Blandit libero volutpat sed cras ornare arcu. Magna eget est lorem ipsum dolor sit amet consectetur. Id neque aliquam vestibulum morbi blandit cursus risus at ultrices.

  <br/>

  Ray: That's great! I think we have a winner!

  <br/>

  Rudraksh: I'm motivated
  <br/>
  Joy: This is a great idea!
  <br/>
  Max: I'm excited to see what you guys come up with!
  <br/>
  Rahul: So, let's get started!
  <br/>
  Ray: Bye!
  <br/>
  Rudraksh: Bye!
`

function* c(){
  const words = content.split(' ')
  // yield words.length
  for(let i = 0; i < words.length; i++){
    yield words[i]
  }
}

const sleep = (ms: number) => new Promise(resolve => setTimeout(resolve, ms))

async function clicked() {
  status.value = 1
  await sleep(1000)
  status.value = 2
  await nextTick()
  video$.value?.play()
  await sleep(600)
  status.value = 3
}

async function startDocMe() {
  status.value = 4
  await sleep(600)
  status.value = 5

  const gen = c()
  let word = gen.next()

  let co = 0
  let open = false
  while(!word.done){
    // random value between 0ms and 5msc
    let t = 0
    if(co < 100) {
      t = Math.random() * (5 + 50)
    } else if (co >= 100 && co < content.split(' ').length - 100){
        t = Math.random() * 0.01 - 0.5
    } else {
      t = Math.random() * (5 + 50)
    }
    await sleep(t)
    word = gen.next()
    const w = word.value!.endsWith(':') ? '<span class="text-slate-800 uppercase font-bold person">' + word.value + '</span>' : word.value
    if(word.value!.includes('<span')){
      open = true
    }
    if(word.value!.endsWith('</span>')){
      open = false
    }
    if(open && p$.value!.innerHTML.endsWith('</span>')){
      // remove </span>
      p$.value!.innerHTML = p$.value!.innerHTML.slice(0, -7)
    } 
    p$.value!.innerHTML += w + ' ' + (open ? '</span>' : '')
    co++
    p$.value?.parentElement!.scrollTo(0, p$.value.parentElement!.scrollHeight)
  }
}
</script>
<style>

.pp span:not(.person) {
  @apply bg-emerald-900 text-white
}

.pp span:not(.person) {
  @apply bg-purple-900 text-white
}

</style>