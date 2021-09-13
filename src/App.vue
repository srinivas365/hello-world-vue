<template>
  <div>
    <!--Binding to text-->
    <h1>{{ greet }} from {{ name }}</h1>

    <!-- v-text: Binding to text using  -->
    <h2 v-text="bind"></h2>

    <!-- v-html: Binding html content from script  -->
    <p v-html="boldText"></p>
    <p v-html="italicText"></p>

    <!-- v-bind: Binding to attributes-->
    <div v-bind:id="headerId">Hello! check this id value</div>
    <br />

    <!-- v-bind: Binding to boolean attributes-->
    <button v-bind:disabled="isDisabled">Bind</button>

    <!-- Binding classes -->
    <h4 v-bind:class="uclass">This is underlined text</h4>
    <h4 v-bind:class="isPromoted && 'promoted'">This is promoted film</h4>
    <h4 v-bind:class="isSoldOut ? 'soldout' : 'new'">
      This is using ternary operator
    </h4>

    <!-- bind multiple classes -->
    <h4 v-bind:class="['new', 'soldout']">new italic, soldout red</h4>

    <!-- conditional binding using object approach-->
    <h4
      v-bind:class="{
        promoted: isPromoted,
        soldout: isSoldOut,
        new: isNew,
      }"
    >
      promoted italic, not soldout red, new underlined film
    </h4>

    <!-- Inline style approach -->
    <h1
      v-bind:style="{
        color: highlightColor,
        'font-size': headersize + 'px',
      }"
    >
      Inline style approach
    </h1>

    <!-- Object style approach -->
    <h1 v-bind:style="headerStyle">Object style approach</h1>
    <h1 v-bind:style="[headerStyle, italicStyle]">Object style approach</h1>

    <!-- conditional rendering -->
    <h2 v-if="num === 0">Number is zero</h2>
    <h2 v-else-if="num < 0">Number is -ve</h2>
    <h2 v-else-if="num > 0">Number is +ve</h2>
    <h2 v-else>Not a Number</h2>

    <!-- for loop of strings -->
    <h2 v-for="(index, name) in names" :key="name">{{ index }} {{ name }}</h2>

    <!-- for loop of object -->
    <h2 v-for="name in fullnames" :key="name.first">
      {{ name.first }} {{ name.last }}
    </h2>

    <!-- for loop of array of arrays -->
    <div v-for="actor in actors" :key="actor.name">
      <h2 :key="actor.name">{{ actor.name }}</h2>
      <li v-for="movie in actor.movies" :key="movie">{{ movie }}</li>
    </div>

    <!-- for loop of properties of an object -->
    <h2 v-for="(value, key, index) in bruce" :key="value">
      {{ index }} {{ key }} {{ value }}
    </h2>

    <!-- for loop of blocked html content -->
    <template v-for="name in names" :key="name">
      <h2>{{ name }}</h2>
      <hr />
    </template>

    <!-- conditonally rendering the elements in loop -->
    <template v-for="num in numbers" :key="num">
      <li v-if="num % 2 == 0">{{ num }}</li>
    </template>

    <!-- functions -->
    <h1>{{ add(2, 3, 4) }}</h1>
    <h1>{{ multiply(3) }}</h1>
    <h1>{{ square(num) }}</h1>

    <!-- events handling -->
    <h1>button click changes this : {{ name }}</h1>
    <button v-on:click="changeName">Click</button>

    <!-- count increment and decrement -->
    <h3>counter : {{ count }}</h3>
    <!-- <button v-on:click="count+=1">increment</button>
    <button v-on:click="count-=1">decrement</button> -->

    <button v-on:click="increment(139, $event)">increment</button>
    <button v-on:click="decrement(139)">decrement</button>
    <button @click="increment(23, $event)">increment</button>
    <button @click="decrement(89)">decrement</button>
    <button @click="changeName($event), increment(1, $event)">
      change name and increment
    </button>
    <br />

    <hr />
    <!-- form handling -->
    <p>{{ formValues.name }}</p>
    <p>{{ formValues.country }}</p>
    <p>{{ formValues.location }}</p>
    <p>Married: {{ formValues.isMarried }}</p>
    <pre>{{ formValues.summary }}</pre>

    <form @submit="submitForm">
      <input type="text" id="name" v-model.trim.lazy="formValues.name" /><br /><br />
      <select name="country" id="country" v-model="formValues.country">
        <option value="India">India</option>
        <option value="America">America</option>
        <option value="UK">UK</option>
        <option value="Australia">Australia</option>
      </select>
      <br /><br />
      <textarea
        name="summary"
        id="summary"
        cols="30"
        rows="10"
        v-model="formValues.summary"
      ></textarea>
      <br /><br />
      <select
        name="location"
        id="location"
        v-model="formValues.location"
        multiple
      >
        <option value="India">India</option>
        <option value="America">America</option>
        <option value="UK">UK</option>
        <option value="Australia">Australia</option>
      </select>

      <div>
        <input
          type="checkbox"
          name="married"
          id="married"            
          v-model="formValues.isMarried"
          true-value="yes"
          false-value="no"
        />
        <label for="married">Married</label>
      </div>

      <div>
        <label for="">Skillset</label>
        <input
          type="checkbox"
          id="html"
          value="html"
          v-model="formValues.skillset"
        />
        <label for="html">HTML</label>
        <input
          type="checkbox"
          id="css"
          value="css"
          v-model="formValues.skillset"
        />
        <label for="css">CSS</label>
        <input
          type="checkbox"
          id="javascript"
          value="javascript"
          v-model="formValues.skillset"
        />
        <label for="javacript">Javascript</label>
      </div>
      <button type="submit">submit</button>
    </form>

    <!-- computed properties -->
    <h1>fullname : {{firstName}} {{lastName}}</h1>
    <h1>fullname : {{fullName}} </h1>
    <h2>total price: {{prices.reduce((total,curr)=>(total=total+curr),0)}}</h2>
    <h2>total price: {{tot_price}}</h2>
    <button @click="addTip()">add tip</button>

    <!-- components and passing attributes to them -->
    <Greet name="Bruce wayne" heroName="Batman" />
    <Greet name="Robert Downey Jr" heroName="Ironman" />
    <Greet name="Jim petersons" heroName="Sheldon" />
    <Greet :name="name" :heroName="heroName" />

    <!-- non-props attributes -->
    <Article id="box" title="Die or Die" desc="This is about Abraham Lincoln" price="hello world"></Article>

    <!-- provide and inject -->
    {{username}}
    <CompA></CompA>

    <!-- custom component events -->
    <button @click="showPopup=true"> show Popup</button>
    <Popup v-show="showPopup" @close="closePopup" />

    <!-- validating emitted events -->

    <!-- components and v-model -->

    <!-- slots -->
    <Card>
      <template v-slot:header>This is header</template>
      <template v-slot:default>This is content</template>
      <template v-slot:footer>This is footer</template>
    </Card>
   <Card>
      <template v-slot:header>This is header</template>
      <template v-slot:default>This is content</template>
      <template v-slot:footer>This is footer</template>
    </Card>

    <!-- Named slots -->

  </div>
</template>

<script>

import Greet from './components/Greet';
import Article from './components/Article'
import CompA from './components/CompA';
import Popup from './components/Popup';
import Card from './components/Card';

export default {
 
  name: "App",
  components: { Greet, Article, CompA, Popup, Card },
  // provide:{
  //   username:"coco-cola thumsup"
  // },
  provide(){
    return {username:this.username}
  },
  data() {
    return {
      showPopup:false,
      username:"coco-cola thumsup",
      formValues: {
        name: "",
        summary: "",
        country: "",
        location: [],
        isMarried: false,
        skillset: [],
        yearsOfExperience: "",
      },
      greet: "Hello world",
      name: "Srinivas",
      heroName:"Shaktimon",
      bind: "This is from v-text directive",
      boldText: "<b> This is from v-html directive </b>",
      italicText: "<i> This is from v-html directive </i>",
      headerId: "box",
      isDisabled: false,
      uclass: "underline",
      isPromoted: true,
      isSoldOut: true,
      isNew: true,
      highlightColor: "orange",
      headersize: 50,
      headerStyle: {
        color: "blue",
        "font-size": "50px",
      },
      italicStyle: {
        "font-style": "italic",
      },
      names: ["bruce", "barry", "harry"],
      fullnames: [
        { first: "Bruce", last: "wayne" },
        { first: "Lily", last: "lynda" },
        { first: "Rose", last: "Jane" },
      ],
      actors: [
        {
          name: "Bruce",
          movies: ["batman", "batman-2", "batman vs superman"],
        },
        {
          name: "Tony stark",
          movies: ["Ironman", "Ironman 2", "Ironman vs Captain america"],
        },
      ],
      bruce: { first: "Bruce", last: "wayne", age: 20, salary: 40000 },
      numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
      baseNum: 251,
      num: 10,
      count: 0,
      firstName:"Bryce",
      lastName:"Wayne",
      prices:[100,200,300]
    };
  },
  methods: {
    closePopup(data){
      this.showPopup=false,
      console.log(JSON.stringify(data))
    },
    add(x, y, z) {
      return x + y + z;
    },
    multiply(x) {
      return x * this.baseNum;
    },
    square(x) {
      return x * x;
    },
    increment(num, event) {
      console.log(event);
      this.count += num;
    },
    decrement(num) {
      this.count -= num;
    },
    changeName(event) {
      console.log(event);
      this.name = "batman";
    },
    submitForm(event){
      event.preventDefault();
      console.log(this.formValues)
    },
    addTip(){
      this.prices.push(100)
    }
  },
  computed:{
    fullName(){
      return `${this.firstName} ${this.lastName}`
    },
    tot_price(){
      return this.prices.reduce((total,curr)=>(total=total+curr),0)
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}

.underline {
  text-decoration: underline;
}

.promoted {
  font-style: italic;
}
.new {
  text-decoration: underline;
}
.soldout {
  color: red;
}
</style>
