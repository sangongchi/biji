### 1.VUE中的form表单元素使用总结

#### 1.select部分

```vue
  <select v-model="gradeId" class="select">
       <option v-for="(item, index) in gradeList" :value="item.value" :key="item.name">								{{item.name}}
       </option>
  </select>
  //v-model 动态绑定 select选中的value值
  
```

#### 2.radio 绑定值

```vue
// 在用户点击的时候做赋值操作
<div v-for="(item,index) in radioList" :key="index" class="col col-xs-12 col-sm-6 col-md-4">
    <input v-show="false" type="radio" name="gender" :value="item.value" :id="item.value" 				      	:checked="sex==item.value" @click="clickRadio(item.value)" />
    	<label :for="item.value">
       {{item.label}}
    </label>
</div>
data(){
	return{
		sex:''
	}
}

methods:{
	  clickRadio(val){
      	this.sex=val;
    },
}
```

#### 3.checkbox

```
<div v-for="item in checkBoxList" :key="item.value" class="col col-xs-12 col-sm-6 col-md-4">
    <label>
        <input v-show="false" @click="clickCheckBox(item.value)" name="Fruit" type="checkbox" 						:value="item.value" :checked="fruit.includes(item.value)" />
        {{item.label}} 
    </label>
</div>


methods:{
	clickCheckBox(val){
      if(this.fruit.includes(val)){
        this.fruit.splice(this.fruit.indexOf(val),1);
      }else{
        this.fruit.push(val);
      }
    }
}
 
```

