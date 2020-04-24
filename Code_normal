<!DOCTYPE html>
<html>
<head>
<title>Task</title>
<style>
    body {
    color: #7F878F;
    background: #999999;
    text-align: center;
    font-family: Helvetica;
}
    header {
    margin: 4px;
    padding: 5px;
    background: #ffeebb;
    border: 1px solid #eebb55;
    border-radius: 7px;
}
    element{
        background:black;
        float:right;
        font-size:15px;
	border-radius: 7px;
    }
    span{
        border: 5px solid black;
        border-style: solid;
        font-size:15px;
        color: white;
        
    }
    #mybtn{
        font-size:30px;
    }
    
    #grids {
    margin: 4px;
    padding: 10px;
    background: #ccccff;
    border: 1px solid #eebb55;
    border-radius: 7px;
    text-align: center;
    left:32%;
    width:670px;
    position:relative;
}

.row {
    display: flex;
    flow-direction:row;
    width:670px;
    font-size:60px;
    text-align: center;
    padding:10px;
}

.grid {
    background: #8888bb;
    color: #FFFFFF;
    border: 10px solid #ccccff;
    border-radius: 5px;
    font-size:60;
    padding:10px;
    text-align: center;
    flex: 100;
}

.grid:hover {
    border-color: #E68B8B;
    color: #E68B8B;
    cursor: pointer;
}
#bestresult{
    border-color: #E68B8B;
    color:black;
    font-size:20px;
}
</style>
</head>
<body>
<header>
    <element>
        <span>Time-</span><span id="min">00:</span><span id="sec">00:</span><span id="ms">00</span>
    </element>

    <element>
        <span>Best Time-</span><span id="Min">00:</span><span id="Sec">00:</span><span id="Ms">00</span>        
    </element>
<h1>Click As Fast As You Can</h1>
<button id="mybtn"> Generate </button>
</header>
<div id="grids"> </div>

<div id="bestresult"> </div>
</body>
<script>
    var stopwatchTimer;
    var minutes=0;
    var seconds=0;
    var milliseconds=0;
    var arr=[],index=0;
    var counter=0;
    var countofsuccess;
    var bestarr=[];



    var prevval=200;

    window.onload=function(){
        document.getElementById("Min").innerHTML=localStorage.getItem("mins",minutes)+":";
        document.getElementById("Sec").innerHTML=localStorage.getItem("secs",seconds)+":";
        document.getElementById("Ms").innerHTML=localStorage.getItem("mils",milliseconds);
    };
    
    document.getElementById("mybtn").addEventListener("click",function(){
        counter++;
        minutes=0;
        seconds=0;
        milliseconds=0;
	if(counter>1) clearInterval(stopwatchTimer);
	startwatch();
    });

    var singledigit=function(num){
        if(num<10) return "0"+num;
        else return num;
    };
    var stopwatch=function(){
        milliseconds+=1;
        if(milliseconds==100){
            seconds+=1;
            milliseconds=0;
        }
        if(seconds==60){
            minutes+=1;
            seconds=0;
        }
        document.getElementById("min").innerHTML=singledigit(minutes)+":";
        document.getElementById("sec").innerHTML=singledigit(seconds)+":";
        document.getElementById("ms").innerHTML=singledigit(milliseconds);
    };
        
    function startwatch(){
        stopwatchTimer=setInterval(stopwatch,10);
    }


    document.getElementById("mybtn").addEventListener("click",function(){
        generate();
    });
    
    function generate(){
        var content="";
        arr=[];
        index=0;
        var num=Math.floor(Math.random()*99);
        for(var i=1;i<=5;i++){
            for(var j=1;j<=5;j++){
                if(j==1){
                    content+="<div class='row'><div class='grid'>" + num + "</div>";
                }
                else if(j==5){
                    content+="<div class='grid' >"+num+"</div></div>"
                }
                else{
                    content+="<div class='grid'>" + num + "</div>";
                }
                arr.push(num);
                num=Math.floor(Math.random()*99);
            }
        }
        document.getElementById("grids").innerHTML=content;
        arr.sort((a,b)=>a-b);
        gridclick();
    }

    
    function gridclick(){
        var ps=document.querySelectorAll(".grid");
        for(var i=0;i<ps.length;i++){
            ps[i].addEventListener('click',hide,false);
        }
    }
    function hide(e){
        if(e.currentTarget.innerHTML==arr[index]){
            index++;
            e.currentTarget.style.visibility='hidden';
        }
        if(index==25){
            var newval=60*minutes + seconds + milliseconds/100;
            if(newval<prevval){
                prevval=newval;
                localStorage.setItem("mins",minutes);
                localStorage.setItem("secs",seconds);
                localStorage.setItem("mils",milliseconds);
                document.getElementById("Min").innerHTML=singledigit(minutes)+":";
                document.getElementById("Sec").innerHTML=singledigit(seconds)+":";
                document.getElementById("Ms").innerHTML=singledigit(milliseconds);
                window.alert("Congrats You make new best score "+singledigit(minutes)+":"+singledigit(seconds)+":"+singledigit(milliseconds));
                clearInterval(stopwatchTimer);
            }
            else{
                window.alert("Congrats "+singledigit(minutes)+":"+singledigit(seconds)+":"+singledigit(milliseconds));
                clearInterval(stopwatchTimer);
            }
            countofsuccess=localStorage.getItem("success")||0;
            countofsuccess++;
            localStorage.setItem("success",countofsuccess);
            bestfive();
            
        }
    }
    
    function bestfive(){
        if(countofsuccess<=5){
            bestarr=[];
            bestarr=JSON.parse(localStorage.getItem("best_five"))||[];
            var data=singledigit(minutes)+":"+singledigit(seconds)+":"+singledigit(milliseconds);
            bestarr.push(data);
            bestarr.sort();
            localStorage.setItem("best_five",JSON.stringify(bestarr));
        }
        else{
            bestarr=[];
            bestarr=JSON.parse(localStorage.getItem("best_five"));
            var data=singledigit(minutes)+":"+singledigit(seconds)+":"+singledigit(milliseconds);
            if(bestarr[4]>data)
            bestarr[4]=data;
            bestarr.sort();
            localStorage.setItem("best_five",JSON.stringify(bestarr));
        }
        bestfiveoutput();
    }
    
    function bestfiveoutput(){
        var content_="Best 5 Times :";
        for(let i=1;i<=bestarr.length;i++){
            content_+="<div>"+ i + " : " + bestarr[i-1]+ "</div>"; 
        }
        document.getElementById("bestresult").innerHTML=content_;
    }
    
 
</script>
</html>
