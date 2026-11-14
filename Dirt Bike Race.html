<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Dirt Bike Race</title>
<style>
:root{--bg:#10151c;--fg:#f4f1ea;--btn:#ffffff22;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
html,body{margin:0;height:100%;background:var(--bg);color:var(--fg);font-family:system-ui,sans-serif;overflow:hidden;touch-action:none}
canvas{display:block;width:100%;height:100%}
#pad{position:fixed;left:0;right:0;bottom:calc(10px + env(safe-area-inset-bottom,0px));display:flex;justify-content:space-between;padding:0 14px;pointer-events:none}
#pad div{display:flex;gap:10px}
#pad button{pointer-events:auto;width:64px;height:64px;border-radius:50%;border:2px solid #fff6;background:var(--btn);color:var(--fg);font-size:20px}
</style>
</head>
<body>
<canvas id="c"></canvas>
<div id="pad">
  <div><button data-k="left">↺</button><button data-k="right">↻</button></div>
  <div><button data-k="brake">■</button><button data-k="gas">▶</button></div>
</div>
<script>
const cv=document.getElementById('c'),ctx=cv.getContext('2d');
let W,H;
function resize(){W=cv.width=innerWidth;H=cv.height=innerHeight}
addEventListener('resize',resize);resize();

const FINISH=18000;
function ramp(x){
  const k=Math.floor((x-1200)/1400);
  if(k<0||k>11)return 0;
  const t=(x-(1200+k*1400))/160;
  if(t>=0&&t<1)return -t*70;
  if(t>=1&&t<1.5)return -70*(1-(t-1)/0.5);
  return 0;
}
function ground(x){
  return 420+55*Math.sin(x/320)+25*Math.sin(x/120)+8*Math.sin(x/40)+ramp(x);
}
function slopeAt(x){return Math.atan2(ground(x+14)-ground(x-14),28)}

// input
const keys={};
addEventListener('keydown',e=>{keys[e.code]=true;if(e.code==='Space'||e.code==='KeyR')if(state==='done')reset();if(e.code.startsWith('Arrow'))e.preventDefault()});
addEventListener('keyup',e=>keys[e.code]=false);
document.querySelectorAll('#pad button').forEach(b=>{
  const k=b.dataset.k;
  b.addEventListener('pointerdown',e=>{keys['pad_'+k]=true;if(state==='done')reset()});
  ['pointerup','pointerleave','pointercancel'].forEach(ev=>b.addEventListener(ev,()=>keys['pad_'+k]=false));
});
const inp=()=>({
  gas:keys.ArrowRight||keys.KeyD||keys.ArrowUp||keys.KeyW||keys.pad_gas,
  brake:keys.ArrowLeft||keys.KeyA||keys.ArrowDown||keys.KeyS||keys.pad_brake,
  rot:((keys.KeyE||keys.pad_right||keys.ShiftRight)?1:0)-((keys.KeyQ||keys.pad_left||keys.ShiftLeft)?1:0)
});

let bikes,state,timer,time,finishOrder;
function mk(name,color,maxS,ai){
  return{name,color,maxS,ai,x:40,y:ground(40)-12,a:0,s:0,vx:0,vy:0,air:false,wr:0,av:0,crash:0,done:false,finTime:0};
}
function reset(){
  bikes=[mk('You','#ff5a36',0,false),mk('Rex','#3aa7ff',9.4,true),mk('Mia','#ffd23a',10.0,true),mk('Bo','#6be28a',10.6,true)];
  bikes.forEach((b,i)=>{b.x=40-i*6;b.y=ground(b.x)-12;b.a=slopeAt(b.x)});
  state='count';timer=200;time=0;finishOrder=[];camY=0;
}
function step(b,i){
  if(b.done){b.s*=0.97;b.x+=b.s;b.y=ground(b.x)-12;b.a=slopeAt(b.x);return}
  if(b.crash>0){b.crash--;if(b.crash===0){b.air=false;b.s=0;b.vx=0;b.vy=0;b.y=ground(b.x)-12;b.a=slopeAt(b.x)}return}
  let c;
  if(b.ai){
    const t=slopeAt(b.x);
    c={gas:b.s<b.maxS+Math.sin(time/40+i)*0.8,brake:false,rot:b.air?Math.sign(slopeAt(b.x+b.vx*10)-b.a)*(Math.abs(slopeAt(b.x+b.vx*10)-b.a)>0.1?1:0):0};
  }else c=inp();
  if(!b.air){
    const t=slopeAt(b.x);
    b.s+=(c.gas?0.22:0)-(c.brake?0.28:0)-0.2*Math.sin(t)-0.02*b.s;
    if(b.s<0)b.s=0;
    b.x+=b.s*Math.cos(t);
    const ny=ground(b.x)-12;
    // launch when ground falls away faster than the bike path
    if(ny>b.y+b.s*Math.sin(t)+3&&b.s>3){
      b.air=true;b.vx=b.s*Math.cos(t);b.vy=b.s*Math.sin(t);b.av=0;
    }else{
      b.y=ny;
      let d=slopeAt(b.x)-b.a;b.a+=d*0.35;
    }
    b.wr+=b.s/12;
  }
  if(b.air){
    b.vy+=0.35;b.vx*=0.999;
    b.x+=b.vx;b.y+=b.vy;
    b.av+=c.rot*0.008;b.av*=0.97;
    b.a+=b.av+c.rot*0.025;
    b.wr+=b.vx/12;
    const gy=ground(b.x)-12;
    if(b.y>=gy){
      const t=slopeAt(b.x);
      let d=((b.a-t)%(Math.PI*2));if(d>Math.PI)d-=Math.PI*2;if(d<-Math.PI)d+=Math.PI*2;
      if(Math.abs(d)>0.95){b.crash=70;b.y=gy;b.a=t+d;b.air=false;b.s=0}
      else{b.air=false;b.y=gy;b.s=Math.max(0,b.vx*Math.cos(t)+b.vy*Math.sin(t))*0.9;b.a=t}
    }
  }
  if(b.x>=FINISH&&!b.done){b.done=true;b.finTime=time;finishOrder.push(b)}
}

let camX=0,camY=0;
function bikeDraw(b){
  ctx.save();
  ctx.translate(b.x-camX,b.y-camY);ctx.rotate(b.a);
  if(b.crash>0)ctx.globalAlpha=0.6+0.4*Math.sin(b.crash);
  const wheel=x=>{
    ctx.save();ctx.translate(x,0);ctx.rotate(b.wr);
    ctx.lineWidth=4;ctx.strokeStyle='#111';ctx.beginPath();ctx.arc(0,0,11,0,7);ctx.stroke();
    ctx.lineWidth=1.5;ctx.strokeStyle='#aaa';
    for(let i=0;i<4;i++){ctx.rotate(Math.PI/4);ctx.beginPath();ctx.moveTo(-10,0);ctx.lineTo(10,0);ctx.stroke()}
    ctx.restore();
  };
  wheel(-20);wheel(20);
  ctx.lineWidth=4;ctx.lineCap='round';ctx.strokeStyle=b.color;
  ctx.beginPath();ctx.moveTo(-20,0);ctx.lineTo(-4,-14);ctx.lineTo(14,-14);ctx.lineTo(20,0);ctx.moveTo(-4,-14);ctx.lineTo(2,0);ctx.lineTo(-20,0);ctx.stroke();
  ctx.strokeStyle='#222';ctx.beginPath();ctx.moveTo(14,-14);ctx.lineTo(11,-24);ctx.lineTo(18,-24);ctx.stroke();
  // rider
  ctx.strokeStyle='#222';ctx.lineWidth=5;
  ctx.beginPath();ctx.moveTo(-5,-16);ctx.lineTo(2,-32);ctx.lineTo(12,-25);ctx.moveTo(-5,-16);ctx.lineTo(8,-8);ctx.stroke();
  ctx.fillStyle=b.color;ctx.beginPath();ctx.arc(4,-39,7,0,7);ctx.fill();
  ctx.fillStyle='#fff';ctx.fillRect(6,-41,5,3);
  ctx.restore();
}

function draw(){
  const p=bikes[0];
  camX=p.x-W*0.3;
  const ty=p.y-H*0.62;camY+=(ty-camY)*0.1;
  // sky
  const g=ctx.createLinearGradient(0,0,0,H);g.addColorStop(0,'#2a4b7c');g.addColorStop(1,'#f2a76b');
  ctx.fillStyle=g;ctx.fillRect(0,0,W,H);
  // parallax hills
  [[0.15,'#4a5f86',220,0.0035],[0.3,'#34476a',140,0.006]].forEach(([f,col,amp,fr])=>{
    ctx.fillStyle=col;ctx.beginPath();ctx.moveTo(0,H);
    for(let x=0;x<=W;x+=8){ctx.lineTo(x,H*0.75-camY*f*0.5+Math.sin((x+camX*f)*fr)*amp*0.3+Math.sin((x+camX*f)*fr*2.7)*amp*0.1-amp*0.2)}
    ctx.lineTo(W,H);ctx.fill();
  });
  // terrain
  ctx.beginPath();ctx.moveTo(0,H+10);
  for(let x=0;x<=W+4;x+=4)ctx.lineTo(x,ground(camX+x)-camY);
  ctx.lineTo(W,H+10);ctx.closePath();
  ctx.fillStyle='#5a3b28';ctx.fill();
  ctx.lineWidth=6;ctx.strokeStyle='#6fb34a';ctx.beginPath();
  for(let x=0;x<=W+4;x+=4){const y=ground(camX+x)-camY;x?ctx.lineTo(x,y):ctx.moveTo(x,y)}
  ctx.stroke();
  // finish line
  const fx=FINISH-camX;
  if(fx>-40&&fx<W+40){
    const fy=ground(FINISH)-camY;
    for(let i=0;i<8;i++){ctx.fillStyle=i%2?'#fff':'#111';ctx.fillRect(fx-4,fy-120+i*15,8,15)}
    ctx.fillStyle='#222';ctx.fillRect(fx-3,fy-120,6,120);
    ctx.fillStyle='#fff';ctx.font='bold 16px system-ui';ctx.fillText('FINISH',fx+10,fy-100);
  }
  // bikes (AI first, player on top)
  for(let i=bikes.length-1;i>=0;i--)bikeDraw(bikes[i]);
  // HUD
  const rank=1+bikes.filter(b=>b!==p&&(b.done?!p.done||b.finTime<p.finTime:(!p.done&&b.x>p.x))).length;
  ctx.fillStyle='#0008';ctx.fillRect(10,10,230,74);
  ctx.fillStyle='#fff';ctx.font='bold 18px system-ui';
  ctx.fillText('Position  '+rank+' / '+bikes.length,22,34);
  ctx.font='14px system-ui';
  ctx.fillText('Time  '+(time/60).toFixed(1)+'s    Speed  '+Math.round(p.s*12)+' km/h',22,56);
  ctx.fillStyle='#fff3';ctx.fillRect(22,64,200,6);ctx.fillStyle='#ff5a36';ctx.fillRect(22,64,200*Math.min(1,p.x/FINISH),6);
  ctx.textAlign='center';
  if(state==='count'){
    ctx.fillStyle='#fff';ctx.font='bold 90px system-ui';
    const n=Math.ceil(timer/60);ctx.fillText(timer<=0?'GO!':n,W/2,H*0.35);
    ctx.font='15px system-ui';ctx.fillText('→ / D gas   ← / A brake   Q / E tilt in the air',W/2,H*0.35+40);
  }
  if(p.crash>0){ctx.fillStyle='#fff';ctx.font='bold 36px system-ui';ctx.fillText('WIPEOUT!',W/2,H*0.3)}
  if(state==='done'){
    ctx.fillStyle='#000b';ctx.fillRect(W/2-170,H*0.2,340,60+finishOrder.length*30+50);
    ctx.fillStyle='#fff';ctx.font='bold 28px system-ui';ctx.fillText('Race results',W/2,H*0.2+40);
    ctx.font='18px system-ui';
    finishOrder.forEach((b,i)=>ctx.fillText((i+1)+'.  '+b.name+'   '+(b.finTime/60).toFixed(1)+'s',W/2,H*0.2+78+i*30));
    ctx.font='14px system-ui';ctx.fillText('Press Space or R to race again',W/2,H*0.2+78+finishOrder.length*30+16);
  }
  ctx.textAlign='left';
}

function loop(){
  if(state==='count'){timer--;if(timer<-40)state='race'}
  else if(state==='race'){
    time++;bikes.forEach(step.bind(null));
    if(bikes[0].done||time>60*120){
      bikes.forEach(b=>{if(!b.done&&time>60*120){b.done=true;b.finTime=time;finishOrder.push(b)}});
    }
    if(bikes[0].done&&bikes.every(b=>b.done||b===bikes[0])&&false){}
    if(bikes[0].done&&time-bikes[0].finTime>120){
      bikes.filter(b=>!b.done).sort((a,b)=>b.x-a.x).forEach(b=>{b.done=true;b.finTime=time;finishOrder.push(b)});
    }
    if(finishOrder.length===bikes.length)state='done';
  }
  draw();requestAnimationFrame(loop);
}
reset();loop();
</script>
</body>
</html>
