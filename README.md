
---
tags: 程式設計_下學期講義,程式設計,第十一章,物件導向與向量 - Class 粒子系統與互動遊戲，教師版,互動藝術程式創作入門,Creative Coding
---
# 11. 學生版_第二個作業- Class 粒子系統與互動遊戲

## 產生多個元件(class)
![](https://s27.aconvert.com/convert/p3r68-cdx67/ugvlc-zwr9f.gif)
```javascript=
function setup() {
  createCanvas(windowWidth, windowHeight);
  shipP=createVector(width/2,height/2)  //預設砲台的位置在視窗的中間
  for(var i=0;i<40;i=i+1){ //i=0,1,2,3,4,5,6... 
    ball = new Obj({}) //產生一個Obj的class元件
    balls.push(ball) //把ball的物件放到balls陣列內
    } 
  
  for(var i=0;i<20;i=i+1){  
   monster = new Monster({}) 
   monsters.push(monster) 
 }
}
```
---
## 你的作答內容

### 以下每個項目，請都要用gif圖片與程式碼表達出來
---

### class的constructor定義內容

#### 執行後的圖片


#### 實際的程式碼

![](https://s27.aconvert.com/convert/p3r68-cdx67/ugvlc-zwr9f.gif)
```javascript=
class Obj{ //宣告一個類別，一個圖案
    constructor(args){ //預設值，基本資料(物件顏色，移動速度，大小，初始顯示位置...)
     //this.p = args.p || {x:random(width),y:random(height)} //描述為該物件的初始位置(x,y) ，||(or)當產生一個物件，有傳給位子參數，則使用該參數，就以日後設定產出
     //this.v = {x:random(-1,1),y:random(-1,1)}//設定一個物件的移動速度 
     this.p = args.p ||createVector(random(width),random(height))
     this.v=createVector(random(-1,1),random(-1,1))
     this.size = random(3,5)  //設定一個物件的放大倍率
     this.color = random(fill_colors)
     this.stroke = random(line_colors)
    }
    draw(){ //畫出單一個物件形狀
      push() //執行push的指令後，依照自己的設定，設定原點(0,0的位置 
       translate(this.p.x,this.p.y)
       scale(this.v.x<0?1:-1,-1)
       fill(this.color)
       stroke(this.stroke)
       strokeWeight(4)//線條粗細
       beginShape()
       for(var k=0;k<points.length;k=k+1){
        
        curveVertex(points[k][0]*this.size,points[k][1]*this.size)
       }
       endShape()
     pop() //執行pop過後，原點(0,0)回到整個視窗的上角
   }

```

---

### class的畫圖程式碼

#### 執行後的圖片


#### 實際的程式碼
![](https://s27.aconvert.com/convert/p3r68-cdx67/ugvlc-zwr9f.gif)

```javascript=
function draw() {
  background(220);
  //for(var j=0;j<balls.length;j=j+1){
  // ball=balls[j]
  // ball.draw()
  // ball.update()
  //}
 if(keyIsPressed){
   if(key=="ArrowLeft"|| key=="a"){
   shipP.x=shipP.x-10

   }
   if(key=="ArrowRight"|| key=="d"){
   shipP.x=shipP.x+10

   }
   if(key=="ArrowUp"|| key=="w"){
   shipP.y=shipP.y-10

   }
   if(key=="ArrowDown"|| key=="s"){
   shipP.y=shipP.y+10

   }

 }

  for(let ball of balls)
  {
    ball.draw()
    ball.update()
    for(let bullet of bullets){
     if(ball.isBallInRanger(bullet.p.x,bullet.p.y)){
     balls.splice(balls.indexOf(ball),1)
     bullets.splice(bullets.indexOf(bullet),1)
     score=score-1
    // elephant_sound.play()
       }  
     }
  }

  for(let bullet of bullets)
  {
    bullet.draw()
    bullet.update()
  }
  for (let monster of monsters) {
   if(monster.dead==true&&monster.timenum>4){
     monsters.splice(monsters.indexOf(monster),1)
   }

    monster.draw();
    monster.update();
    for (let bullet of bullets) {
      if (monster.isBallInRanger(bullet.p.x, bullet.p.y)) {
        //monsters.splice(monsters.indexOf(monster), 1);  // 从数组中移除被击中的大象
        bullets.splice(bullets.indexOf(bullet), 1);
        score = score + 1;
        monster.dead = true
      }
    }
  }
  
```

---

### class的移動內容

#### 執行後的圖片


#### 實際的程式碼
![](https://s27.aconvert.com/convert/p3r68-cdx67/ugvlc-zwr9f.gif)

```javascript=
update(){ //計算出移動元件後的位置
        this.p.add(this.v)
        if(this.p.x<=0 || this.p.x>width){ //x軸碰到左邊(<=0)，，或是碰到右邊(>width)
            this.v.x = -this.v.x //把x方向速度改變
         }
         if(this.p.y<=0 || this.p.y>height){ //y軸碰到上邊(<=0)，，或是碰到下邊(>height)
            this.v.y = -this.v.y //把y方向速度改變
         }
       }
    
      

```

---

### 產生20個相同class的元件

#### 執行後的圖片


#### 實際的程式碼
![](https://s33.aconvert.com/convert/p3r68-cdx67/1o00l-c0p2c.gif)
```javascript=
function setup() {
  createCanvas(windowWidth, windowHeight);
  shipP=createVector(width/2,height/2)  //預設砲台的位置在視窗的中間
  for(var i=0;i<40;i=i+1){ //i=0,1,2,3,4,5,6... 
    ball = new Obj({}) //產生一個Obj的class元件
    balls.push(ball) //把ball的物件放到balls陣列內
    } 
  
  for(var i=0;i<20;i=i+1){  
   monster = new Monster({}) 
   monsters.push(monster) 
 }
}
```

---

### 元件的大小，元件的左右移動，速度不一

#### 執行後的圖片


#### 實際的程式碼
![](https://s27.aconvert.com/convert/p3r68-cdx67/ugvlc-zwr9f.gif)

```javascript=
 update() {
    //this.p.x = this.p.x+this.v.x //x軸目前位置加上x軸的移動速度
    //this.p.y = this.p.y+this.v.y
    this.p.add(this.v)//上面兩行的效果

     if(this.p.x<=0||this.p.x>=width){
     this.v.x=-this.v.x  
    }
     if(this.p.y<=0||this.p.y>=height){
     this.v.y=-this.v.y
     }
  }

```

---




## 滑鼠按下之後，消失不見

![](https://hackmd.io/_uploads/ByzH1Az73.gif)
```javascript=
isBallInRanger(x,y){ //功能:判斷滑鼠按下的位置是否在物件範圍內
    let d = dist(x,y,this.p.x,this.p.y) //計算兩個點之間的具距離
    if (d<5*this.size){
     return true  //滑鼠與物件的距離小於物件的寬度，代表碰觸了，則傳回rue的值
    }else{
      return false
    }    
  }

```

---

## 發射子彈

---
![](https://s31.aconvert.com/convert/p3r68-cdx67/hmefn-6830i.gif)

```javascript=
bullet = new Bullet({}) //在滑鼠按下的地方，產生一個新的bullet class元件
bullets.push(bullet)
--------------------------------------------------------
子彈的程式碼
class Bullet{
    constructor(args){
      this.r = args.r || 20 //設計的飛彈有大有小時，就傳參數args.r來設定飛彈大小，沒有參數就已10為主
      this.p = args.p || shipP.copy()//createVector(width/2,height/2)//建立一個向量{x:width/2,y:height/2}
      this.v = args.v || createVector(mouseX-width/2,mouseY-height/2).limit(20)
      this.color = args.color || "white"
     }
     draw(){ //匯出物件程式碼
       push()
        translate(this.p.x,this.p.y)
        fill(this.color)
        noStroke()
        ellipse(0,0,this.r)
       pop()
     }
     update(){   //計算移動後的位子
      this.p.add(this.v) 
     }
   }
   
```

## 物件消失不見
![](https://s27.aconvert.com/convert/p3r68-cdx67/9o41y-zokzj.gif)

---
```javascript=
 for(let ball of balls)
  {
    ball.draw()
    ball.update()
    for(let bullet of bullets){
     if(ball.isBallInRanger(bullet.p.x,bullet.p.y)){
     balls.splice(balls.indexOf(ball),1)
     bullets.splice(bullets.indexOf(bullet),1)
     score=score-1
    // elephant_sound.play()
       }  
     }
  }

  for(let bullet of bullets)
  {
    bullet.draw()
    bullet.update()
  }
  for (let monster of monsters) {
   if(monster.dead==true&&monster.timenum>4){
     monsters.splice(monsters.indexOf(monster),1)
   }

    monster.draw();
    monster.update();
    for (let bullet of bullets) {
      if (monster.isBallInRanger(bullet.p.x, bullet.p.y)) {
        
        bullets.splice(bullets.indexOf(bullet), 1);
        score = score + 1;
        monster.dead = true
      }
    }
  }

```

## 計算得分


---
![](https://s19.aconvert.com/convert/p3r68-cdx67/8e0f6-igfdz.gif)
```javascript=

  textSize(50)
  text(score,50,50)
  push() //重新規劃原點，在視窗中間
   let dx = mouseX - width/2
   let dy = mouseY - height/2 
   let angle = atan2(dy,dx)
   translate(shipP.x,shipP.y)
   fill("yellow")
   noStroke()
   rotate(angle-300)
   triangle(-25,25,25,25,0,-50) //設定三個點畫成一個三角形
   ellipse(0,0,40)
  pop() //恢復原本設定，原點(0,0)在視窗的左上角
--------------------------------------------------------
在物件下會有score = score + 1 or -1
}

```

## 結束後顯示畫面
![](https://s31.aconvert.com/convert/p3r68-cdx67/fv1f4-t7h6i.gif)
11. 學生版_第二個作業- Class 粒子系統與互動遊戲.md
目前顯示的是「11. 學生版_第二個作業- Class 粒子系統與互動遊戲.md」。




