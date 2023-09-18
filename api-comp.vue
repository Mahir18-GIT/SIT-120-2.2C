<!-- MyComponent.vue -->
<!-- 1. Template Syntax -->
<template>
    <!-- 1a. Text Interpolation -->
    <p>{{ message }}</p>
  
    <!-- 1b. Raw HTML [v-html] -->
    <div v-html="rawHtml"></div>
  
    <!-- 1c. Attribute Bindings [v-bind:id] -->
    <div v-bind:id="dynamicId">This div has a dynamic ID</div>
  
    <!-- 1d. JavaScript expressions inside syntax {{ }} -->
    <p>{{ 2 + 2 }}</p>
    <p>{{ message.split('').reverse().join('') }}</p>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    name: 'MyComponent',
    setup() {
      // Reference to a reactive variable
      const message = ref('Hello Vue 3!');
      const rawHtml = ref('<span style="color: red">This is raw HTML</span>');
      const dynamicId = ref('myDynamicId');
  
      return {
        message,
        rawHtml,
        dynamicId
      }
    }
  }
  </script>

  
  <!-- MethodsComponent.vue -->

<template>
    <div>
      <!-- Button to trigger the method -->
      <button @click="greetUser">Click me to greet!</button>
  
      <!-- Show the greeting message -->
      <p>{{ greetingMessage }}</p>
  
      <!-- Using method to compute and display a message -->
      <p>{{ reversedMessage() }}</p>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    name: 'MethodsComponent',
    setup() {
      const greetingMessage = ref('');
  
      // 2. Methods
      const greetUser = () => {
        greetingMessage.value = 'Hello, Vue 3 user!';
      };
  
      const reversedMessage = () => {
        return greetingMessage.value.split('').reverse().join('');
      };
  
      return {
        greetUser,
        greetingMessage,
        reversedMessage
      }
    }
  }
  </script>
  


<!-- 3. Reactivity Fundamentals
a. ref() -->

  <template>
    <button @click="incrementCount">Click me!</button>
    <p>You have clicked {{ count }} times.</p>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup() {
      // Create a reactive reference for count
      const count = ref(0);
  
      // A method to increment the count
      const incrementCount = () => {
        count.value++;
      };
  
      return {
        count,
        incrementCount
      }
    }
  }
  </script>
  
 
<!-- b. Script Setup -->
<template>
  <button @click="incrementCount">Click me!</button>
  <p>You have clicked {{ count }} times.</p>
</template>

<script setup>
import { ref } from 'vue';

// Directly declare a reactive reference
const count = ref(0);

const incrementCount = () => {
  count.value++;
};
</script>

<!-- 4. Computed Properties -->
<template>
    <p>Full Name: {{ fullName }}</p>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue';
  
  const firstName = ref('John');
  const lastName = ref('Doe');
  
  // Computed property
  const fullName = computed(() => {
    return `${firstName.value} ${lastName.value}`;
  });
  </script>
<!--   
  5. Class and Style Bindings

  a. Binding HTML class [v-bind:class]

  Object Syntax: -->
  <template>
    <div :class="{ active: isActive, 'text-danger': hasError }"></div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const isActive = ref(true);
  const hasError = ref(false);
  </script>
 
 <!-- Array Syntax: -->
 <template>
    <div :class="[activeClass, errorClass]"></div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const activeClass = ref('active');
  const errorClass = ref('text-danger');
  </script>
  
  <!-- b. Binding Inline Styles (v-bind:style): -->

  <!-- Object Syntax: -->

  <template>
    <div :style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const activeColor = ref('red');
  const fontSize = ref(30);
  </script>

<!-- Array Syntax: -->
<template>
    <div :style="[baseStyles, overridingStyles]"></div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const baseStyles = ref({
    color: 'red',
    fontSize: '20px'
  });
  
  const overridingStyles = ref({
    fontSize: '25px'
  });
  </script>

<!-- 6. List Rendering -->
<!-- a. v-for with an Object -->
<template>
    <ul>
      <li v-for="(value, key) in object" :key="key">{{ key }}: {{ value }}</li>
    </ul>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const object = ref({
    firstName: 'John',
    lastName: 'Doe',
    age: 30
  });
  </script>

<!-- b. v-for with a Range:   -->
<template>
    <ul>
      <li v-for="n in 5">{{ n }}</li>
    </ul>
  </template>

<!-- c. v-for on <template>: -->
    <template>
        <template v-for="item in items">
          <li :key="item.id">{{ item.text }}</li>
        </template>
      </template>
      
      <script setup>
      import { ref } from 'vue';
      
      const items = ref([{ id: 1, text: 'Item 1' }, { id: 2, text: 'Item 2' }]);
      </script>

<!-- d. v-for with v-if: -->
<template>
    <ul>
      <li v-for="item in items" :key="item.id" v-if="item.isActive">{{ item.text }}</li>
    </ul>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const items = ref([{ id: 1, text: 'Item 1', isActive: true }, { id: 2, text: 'Item 2', isActive: false }]);
  </script>

<!-- e. v-for with a Component: -->
<template>
    <item-component v-for="item in items" :key="item.id" :data="item" />
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import ItemComponent from './ItemComponent.vue';
  
  const items = ref([{ id: 1, text: 'Item 1' }, { id: 2, text: 'Item 2' }]);
  </script>

<!-- 7. Event Handling: -->
<!-- a. Inline Handlers: -->
<template>
    <button @click="count += 1">Click me!</button>
    <p>You have clicked {{ count }} times.</p>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const count = ref(0);
  </script>

<!-- b. Method Handlers: -->
<template>
    <button @click="incrementCount">Click me!</button>
    <p>You have clicked {{ count }} times.</p>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const count = ref(0);
  
  const incrementCount = () => {
    count.value++;
  }
  </script>
  
<!-- 8. Form Input Bindings:
a. Various v-model: -->
<template>
    <input type="text" v-model="text" />
    <input type="checkbox" v-model="checkbox" />
    <input type="radio" v-model="radio" value="A" /> A
    <input type="radio" v-model="radio" value="B" /> B
    <select v-model="selected">
      <option>A</option>
      <option>B</option>
    </select>
    <textarea v-model="textarea"></textarea>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const text = ref('');
  const checkbox = ref(false);
  const radio = ref('');
  const selected = ref('');
  const textarea = ref('');
  </script>

<!-- b. v-model modifiers: -->
<template>
    <input type="text" v-model.lazy="text" />
    <input type="text" v-model.number="numberInput" />
    <input type="text" v-model.trim="trimmedInput" />
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const text = ref('');
  const numberInput = ref('');
  const trimmedInput = ref('');
  </script>

<!-- 9. Watchers: -->
<template>
    <input v-model="query" />
  </template>
  
  <script setup>
  import { ref, watch } from 'vue';
  
  const query = ref('');
  
  watch(query, (newValue, oldValue) => {
    console.log(`Query changed from ${oldValue} to ${newValue}`);
  });
  </script>

<!-- 10. Components:
a. Props:
ChildComponent.vue -->
<template>
    <p>{{ text }}</p>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps(['text']);
  </script>

<!-- 
6. List Rendering:
a. v-for with an Object: -->

<template>
  <ul>
    <li v-for="(value, key) in object" :key="key">{{ key }}: {{ value }}</li>
  </ul>
</template>

<script setup>
import { ref } from 'vue';

const object = ref({
  firstName: 'John',
  lastName: 'Doe',
  age: 30
});
</script>
<!-- b. v-for with a Range: -->

<template>
  <ul>
    <li v-for="n in 5">{{ n }}</li>
  </ul>
</template>
<!-- c. v-for on <template>:
vue
Copy code -->
<template>
  <template v-for="item in items">
    <li :key="item.id">{{ item.text }}</li>
  </template>
</template>

<script setup>
import { ref } from 'vue';

const items = ref([{ id: 1, text: 'Item 1' }, { id: 2, text: 'Item 2' }]);
</script>
<!-- d. v-for with v-if: -->

<template>
  <ul>
    <li v-for="item in items" :key="item.id" v-if="item.isActive">{{ item.text }}</li>
  </ul>
</template>

<script setup>
import { ref } from 'vue';

const items = ref([{ id: 1, text: 'Item 1', isActive: true }, { id: 2, text: 'Item 2', isActive: false }]);
</script>
<!-- e. v-for with a Component: -->
<template>
  <item-component v-for="item in items" :key="item.id" :data="item" />
</template>

<script setup>
import { ref } from 'vue';
import ItemComponent from './ItemComponent.vue';

const items = ref([{ id: 1, text: 'Item 1' }, { id: 2, text: 'Item 2' }]);
</script>
<!-- 7. Event Handling:
a. Inline Handlers: -->

<template>
  <button @click="count += 1">Click me!</button>
  <p>You have clicked {{ count }} times.</p>
</template>

<script setup>
import { ref } from 'vue';

const count = ref(0);
</script>
<!-- b. Method Handlers: -->

<template>
  <button @click="incrementCount">Click me!</button>
  <p>You have clicked {{ count }} times.</p>
</template>

<script setup>
import { ref } from 'vue';

const count = ref(0);

const incrementCount = () => {
  count.value++;
}
</script>
<!-- 8. Form Input Bindings:
a. Various v-model: -->

<template>
  <input type="text" v-model="text" />
  <input type="checkbox" v-model="checkbox" />
  <input type="radio" v-model="radio" value="A" /> A
  <input type="radio" v-model="radio" value="B" /> B
  <select v-model="selected">
    <option>A</option>
    <option>B</option>
  </select>
  <textarea v-model="textarea"></textarea>
</template>

<script setup>
import { ref } from 'vue';

const text = ref('');
const checkbox = ref(false);
const radio = ref('');
const selected = ref('');
const textarea = ref('');
</script>
<!-- b. v-model modifiers: -->

<template>
  <input type="text" v-model.lazy="text" />
  <input type="text" v-model.number="numberInput" />
  <input type="text" v-model.trim="trimmedInput" />
</template>

<script setup>
import { ref } from 'vue';

const text = ref('');
const numberInput = ref('');
const trimmedInput = ref('');
</script>

<!-- 9. Watchers: -->

<template>
  <input v-model="query" />
</template>

<script setup>
import { ref, watch } from 'vue';

const query = ref('');

watch(query, (newValue, oldValue) => {
  console.log(`Query changed from ${oldValue} to ${newValue}`);
});
</script>

<!-- 10. Components:
a. Props:
ChildComponent.vue -->

<template>
  <p>{{ text }}</p>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps(['text']);
</script>

<!-- b. Events:
ChildComponent.vue -->
<template>
  <button @click="emitEvent">Click me!</button>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const emit = defineEmits(['custom-event']);

const emitEvent = () => {
  emit('custom-event', 'Data from child');
}
</script>

<!-- c. Slots:
ChildComponent.vue -->
<template>
  <slot name="header"></slot>
</template> 
