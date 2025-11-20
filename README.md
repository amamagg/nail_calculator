# 美甲計算機

用來解決老是算錯錢的症頭!  

常見的價目表可分為四種類型,將會依不同類型進行計算  
*  固定項目: 單色/貓眼/漸層/法式...

```
   <div class="服務項目">
	    <input type="checkbox" id="凝膠_法式" data-price="1500">
            <label for="凝膠_法式">法式</label>
            <span class="價格">1500 元</span>         
   </div>
```

*  浮動項目: 跳色/延甲...

-放在CSS的地方
```
    <div class="服務項目">            
            <input type="checkbox" id="浮動跳色" data-price="100"> 
            <label for="浮動跳色">跳色</label>
			<div class="浮動項目">
               <input type="number" id="浮動跳色_數量" value="1" min="1" max="10">
            <span class="價格">x100 元/色</span>
			</div>
		</div>
```

-放在JAVASCRIPT的地方
     
```

//2. 處理浮動項目
//跳色
                    else if( checkbox.id ==('浮動跳色')){                     
                        const 數量 = parseInt(document.getElementById('浮動跳色_數量').value) || 1;     
                        const 金額 = 項目金額 * 數量;                        
                        明細類別['凝膠'].push({ label: `${項目名稱} x ${數量}`, price: 金額 });
                        總金額 += 金額;
                    }
```
*  自訂項目: 手繪/異素材...

需要更新CSS及JS (以下為CSS範例的部分)
```
<h3>造型</h3>
      		<div id="自訂項目區">
            </div>
        <div class="自訂項目">
            <div class="自訂項目內容">
                <input type="text" id="自訂項目名稱" placeholder="名稱">
                <input type="number" id="自訂項目單價" placeholder="單價">
                <span> x </span>
                <input type="number" id="自訂項目數量" value="1" min="1">
            </div>
            <button id="自訂項目按鈕" onclick="功能_新增自訂項目()">新增</button>
        </div>
```
*  活動: 折扣/折價券

-放在CSS的地方
```
    <h3>折扣</h3>
		<div class="服務項目">
            <input type="checkbox" id="折扣_九折" value="0.9"> 
            <label for="折扣_九折">九折優惠</label>            
        </div>
        <div class="浮動項目">
            <input type="checkbox" id="折價券"> 
            <label for="折價券">折價券</label>
             <input type="number" id="折價券金額" value="100">             
		</div>  
```

-放在JAVASCRIPT的地方
```
// 4. 折扣(需要設立條件)        
//若有折價券先折,再打折
            const 折扣_折價券 = document.getElementById('折價券');
            if (折扣_折價券.checked) {     
                const 折價券金額 = parseInt(document.getElementById('折價券金額').value) || 1;
                const 折價券名稱 = document.querySelector('label[for="折價券"]').textContent;                              
                明細類別['折扣'].push({label: 折價券名稱,price:折價券金額 });
                總金額 -= 折價券金額;
            }
            //打折
            const 折扣_九折 = document.getElementById('折扣_九折');
            if (折扣_九折.checked) {     
                const 折扣_折數 = parseFloat(折扣_九折.value);
                const 折扣名稱 = document.querySelector('label[for="折扣_九折"]').textContent;                              
                明細類別['折扣'].push({ label:折扣名稱 });
                總金額 *= 折扣_折數;
            }
```

註
* 新增類別

-放在CSS的地方
 
     ```
     <h3>保養</h3>
     ```

-放在JAVASCRIPT的地方 (明細最後呈現的順序,如要更改順序記得中間都要有","，最後一個沒有逗號)
```
//找到這個項目,新增[保養]類別上去
                 const 明細類別 = {
                '凝膠': [],
                '自訂': [],
                '保養': [],
                '卸甲': [],
                '折扣': []
            };

```
