```
//继承
function inherits(ctor,superCtor){
	ctor.super_ = superCtor;
	ctor.prototype = Object.create(superCtor.prototype,{
		constructor : {
			value : ctor,
			emumerable : false,
			writable : true,
			configurable : true
		}
	})
};


var Person = function(name){
	this.name = name;
};


Person.prototype.sayName = function(){
	console.log("Hi my name is "+this.name);
};

Person.prototype.shoutName = function(){
	console.log("Hi my name is "+this.name + "!");
};

/*Person.sayName = function(){
	console.log("Hi my name is "+this.name);
}*/

var john = new Person("john");
var bobby = new Person("bobby");

john.sayName(); // Hi my name is john
bobby.shoutName(); // Hi my name is bobby!


john.name = "johnny";


var Friend = function(name,instrument){
	Friend.super_.call(this, name);
	this.instrument = instrument;
}
inherits(Friend, Person);


Friend.prototype.getInstrument = function(){
	console.log(this.instrument);
}


var julia = new Friend("julia",'trombone');

julia.sayName();
julia.getInstrument();

//实现继承的方法
var human = {
	species : "human",//复制函数
	create : function(values){
		var instnce = Object.create(this);
		Object.keys(values).forEach(function(key){
			instnce[key] = values[key];
		})
		return instnce;
	},
	saySpecies : function(){
		console.log(this.species);
	},
	sayName : function(){
		console.log(this.name)
	}
};

/*var musician = Object.create(human);*/

var musician = human.create({
	species : "musician",
	playInstrument : function(){
		console.log("plays " + this.instrument);
	}
})
var will = musician.create({
	name : "Will",
	instrument : "drums"
});

will.playInstrument();
will.sayName();
```




