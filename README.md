# getLabelFromId

```
function getPt()
{
   
    var form = document.getElementById('updateTable');
    console.log(form);


    var inputNodes = form.getElementsByTagName('*');
    var map = new Map();
    for(var i = 0; i < inputNodes.length; ++i)
    {
         var inputNode1 = inputNodes[i];
         var inputVale = inputNode1.value;
//console.log("inputVale== "+inputVale);
         var inputName = inputNode1.name;
//console.log("inputName== "+inputName);
         var innerHTMl = inputNode1.innerHTML;
//console.log("innerHTMl== "+innerHTMl);
    var innerTexT = inputNode1.innerText;
console.log("innerTexT== "+innerTexT);
         map.set(inputName,inputVale);
    }
    for (const [key, value] of map.entries())
    {
         console.log("Map Values :: "+ `${key} = ${value}`);
    }

    var formData = new FormData(form);
    console.log(formData);
    var objFormEntries = Object.fromEntries(formData);
    console.log("objFormEntries= "+objFormEntries);
    var strJson = JSON.stringify(Object.fromEntries(formData));
    console.log("strJson= "+strJson);
    var modOb = Object.keys(objFormEntries).reduce(function(p, c)
    {
        return p.concat([encodeURIComponent(c) + "=" + encodeURIComponent(objFormEntries[c])]);
    }, []);
   
    console.log("modOb= "+modOb);
    var urlEncodedData = modOb.join("&").replace(/%20/g, "+");  
    console.log("urlEncodedData= "+urlEncodedData);
}
```

https://youtu.be/mPPhcU7oWDU

https://www.baeldung.com/spring-jdbctemplate-in-list

https://stackoverflow.com/q/10606229

https://www.baeldung.com/sql-injection

https://www.tabnine.com/code/java/methods/org.springframework.jdbc.core.namedparam.NamedParameterJdbcTemplate/queryForObject


```


function getPt2()
{
    var jsonObj ={};
    var form = document.getElementById('getJson');
    var inputNodes = form.querySelectorAll("mat-label,table,mat-expansion-panel, thead, tbody, th, tr, td,select, label, h4, mat-card-subtitle, button, div:not(.mat-select-value):not(.mat-paginator-range-actions):not(.mat-paginator-range-label):not(i)");
    /*var inputNodes = form.querySelectorAll("span");
    var inputNodes = form.querySelectorAll('*:not(input):not(select)');
    var inputNodes = form.getElementsByTagName('*');
   
    var filteredNodes = [];
    for (var i = 0; i < inputNodes.length; i++)
    {
        var currentNode = inputNodes[i];
        if (!currentNode.closest('.mat-paginator-range-label'))
        {
            filteredNodes.push(currentNode);
        }
        else
        {
            console.log("got it");
        }
    }*/
   
    for(var i = 0; i < inputNodes.length; i++)
    {
        var inputNode1 = inputNodes[i];
        var outerTexT = inputNode1.outerText;
        const relsArray = outerTexT.split(/\r\n|\n|\r/);
                /*space (' ')
                tab (\t)
                carriage return (\r)
                line feed (\n), and
                vertical tab (\v)*/
       
        for(var j=0; j < relsArray.length; j++)
        {
            const conVal = relsArray[j];
            var firstRep = conVal.replace("#", "");
            if(firstRep===undefined || firstRep.indexOf("\t") !== -1 || firstRep === "" || firstRep === null || firstRep.match(/^ *$/) !== null || firstRep.trim() === '' || firstRep === "print")
            {
                continue;
            }
            else
            {
                let key = capitalizeAfterSpace(conVal);
                for(var k=0; k <key.length; k++)
                {
                    if(containsWhitespace(key))
                    {
                    key = key.trim();
                    key = replaceChars(key);
                    }
                    else
                    {
                    continue;
                    }
                }
               
                var value = conVal.charAt(0).toUpperCase() + relsArray[j].slice(1);
                key = key.charAt(0).toLowerCase() + key.slice(1);
               
                if(!jsonObj.hasOwnProperty(key))
                {
                    key = replaceChars(key);
                    value = replaceChars(value);
                    jsonObj[key] = value;
                }
            }
        }
        var lastVal = JSON.stringify(jsonObj);
        console.log(lastVal);
    }
}


function containsWhitespace(str)
{
    return /\s/.test(str);
}


function replaceChars(keyValus)
{
    keyValus = allReplace(keyValus,
        {
            'navigate_beforeBack':'back',
            'Navigate_beforeBack' : "Back",
            'nextnavigate_next' : 'next',
            'Nextnavigate_next' : 'Next',
            'nextNavigate_next' : 'next',
            'Next navigate_next' : 'Next',
            'add_circle' : '',
            'Add_circle' : '',
            'descriptionUploadFiles' : 'uploadFiles',
            'Description Upload Files' : 'Upload Files',
            '\\#' : '',
            '\\*' : ''
        });
   
    // keyValus = keyValus.replace("navigate_beforeBack", "back");
   
    return keyValus;
}

function allReplace(str, obj)
{
    for (const x in obj)
    {
        if (x.search('[a-z]\\.\\+\\*\\#') != -1)
        {
            console.log(x);
        }
        str = str.replace(new RegExp(x, 'g'), obj[x]);
    }
    return str;
}


function capitalizeAfterSpace(conVal)
{
    let key = "";
    let capitalizeNext = false;

    for (let i = 0; i < conVal.length; i++)
    {
        const char = conVal[i];
        if (char === " ")
        {
            capitalizeNext = true;
        }
        else if (capitalizeNext)
        {
            key += char.toUpperCase();
            capitalizeNext = false;
        }
        else
        {
            key += char;
        }
    }
    return key;
}


```

https://www.tradingview.com/pine/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © silvershinesarath

//@version=6
indicator("Comprehensive Candlestick Strategy", overlay=true)

// --- Helper Functions ---
abs(x) => x >= 0 ? x : -x

// --- Candlestick Patterns ---
// Bullish Patterns
bullishEngulfing = close[1] < open[1] and close > open and close > open[1] and open < close[1]
bullishHarami = close > open and close[1] < open[1] and open > close[1] and close < open[1]
tweezerBottom = low[1] == low and close > open
morningStar = close[2] < open[2] and close[1] < open[1] and close > open and close > open[2]

bullishAbandonedBaby = close[2] < open[2] and open[1] < close[2] and close > open[2]
threeOutsideUp = close[2] < open[2] and close[1] > open[1] and close > open
threeInsideUp = close[2] < open[2] and close[1] < open[1] and close > open[2]
bullishKicker = close > open and open[1] > close[1] and open > close[1]
piercingLine = close > open and close[1] < open[1] and close > open[1] and open < close[1]
hammer = close > open and high - low > 3 * (open - close) and close - low < 0.2 * (high - low)
invertedHammer = open > close and high - low > 3 * (close - open) and high - close < 0.2 * (high - low)

// Bearish Patterns
bearishEngulfing = close[1] > open[1] and close < open and close < open[1] and open > close[1]
bearishHarami = close < open and close[1] > open[1] and open < close[1] and close > open[1]
tweezerTop = high[1] == high and close < open
eveningStar = close[2] > open[2] and close[1] > open[1] and close < open and close < open[2]

bearishAbandonedBaby = close[2] > open[2] and open[1] > close[2] and close < open[2]
threeOutsideDown = close[2] > open[2] and close[1] < open[1] and close < open
threeInsideDown = close[2] > open[2] and close[1] > open[1] and close < open[2]
hangingMan = open > close and high - low > 2 * (close - open) and high - close < 0.2 * (high - low)
bearishKicker = close < open and open[1] < close[1] and open < close[1]
darkCloudCover = close < open and close[1] > open[1] and close < open[1] and open > close[1]
shootingStar = open < close and high - low > 2 * (open - close) and close - low < 0.2 * (high - low)
threeBlackCrows = close < open and close[1] < open[1] and close[2] < open[2] and close < close[1] and close[1] < close[2]

// Additional Patterns
risingThree = close[4] < open[4] and close > open[4] and close[1] < open[1] and close[2] < open[2] and close[3] < open[3]
fallingThree = close[4] > open[4] and close < open[4] and close[1] > open[1] and close[2] > open[2] and close[3] > open[3]
tasukiGap = close[2] > open[2] and open[1] > close[1] and close[1] > open
matHold = close[4] > open[4] and close[3] > open[3] and close[2] < open[2] and close > open
insideBars = high[1] < high[2] and low[1] > low[2]
threeWhiteSoldiers = close > open and close[1] > open[1] and close[2] > open[2] and close > close[1] and close[1] > close[2]
marubozu = open == low and close == high or open == high and close == low
doji = abs(close - open) <= 0.1 * (high - low)
gravestoneDoji = open == high and close == low
dragonflyDoji = open == low and close == high
longLeggedDoji = abs(open - close) <= 0.03 * (high - low)
bullishSpinningTop = abs(close - open) < 0.5 * (high - low) and close > open
bearishSpinningTop = abs(close - open) < 0.5 * (high - low) and close < open
triStar = doji[2] and doji[1] and doji
longWicks = abs(high - close) > 2 * abs(open - close) or abs(low - close) > 2 * abs(open - close)

morningStarDoji = doji[1] and close > open[2] and close > open[2]
eveningStarDoji = doji[1] and close < open[2] and close < open[2]

// --- Moving Averages ---
sma50 = ta.sma(close, 50)
sma200 = ta.sma(close, 200)
ema50 = ta.ema(close, 50)
ema200 = ta.ema(close, 200)

// --- RSI ---
rsiPeriod = 14
rsiValue = ta.rsi(close, rsiPeriod)
rsiOverbought = 70
rsiOversold = 30
stochK = ta.stoch(close, high, low, 14)
stochD = ta.sma(stochK, 3)

// --- Stochastic RSI ---
stochRSI = (rsiValue - ta.lowest(rsiValue, 14)) / (ta.highest(rsiValue, 14) - ta.lowest(rsiValue, 14))
stochOverbought = 0.8
stochOversold = 0.2

// --- MACD ---
[macdLine, signalLine, _] = ta.macd(close, 12, 26, 9)
macdHist = macdLine - signalLine

// --- Support and Resistance Detection ---
pivotHigh = ta.valuewhen(high > high[1] and high > high[2], high, 0)
pivotLow = ta.valuewhen(low < low[1] and low < low[2], low, 0)

// --- Bollinger Bands ---
bbPeriod = 20
bbDev = 2.0
basis = ta.sma(close, bbPeriod)
bbUpper = basis + bbDev * ta.stdev(close, bbPeriod)
bbLower = basis - bbDev * ta.stdev(close, bbPeriod)

// --- Trend Confirmation ---
isUptrend = close > sma50 and sma50 > sma200
isDowntrend = close < sma50 and sma50 < sma200

// --- Parabolic SAR ---
sar = ta.sar(0.02, 0.02, 0.2)

// --- Volume Analysis ---
volMA = ta.sma(volume, 20)
highVolume = volume > volMA

// --- Buy and Sell Conditions ---
buySignal = bullishEngulfing or bullishHarami or tweezerBottom or morningStar or morningStarDoji or bullishAbandonedBaby or threeOutsideUp or threeInsideUp or bullishKicker or piercingLine or hammer or invertedHammer or threeWhiteSoldiers
sellSignal = bearishEngulfing or bearishHarami or tweezerTop or eveningStar or eveningStarDoji or bearishAbandonedBaby or threeOutsideDown or threeInsideDown or hangingMan or bearishKicker or darkCloudCover or shootingStar or threeBlackCrows


// --- Plot Buy and Sell Signals ---
plotshape(series=buySignal, location=location.belowbar, color=color.green, style=shape.labelup, title="Buy Signal", text="BUY")
plotshape(series=sellSignal, location=location.abovebar, color=color.red, style=shape.labeldown, title="Sell Signal", text="SELL")

// --- Plot Trend Confirmation ---
plot(sma50, color=color.blue, title="50 SMA")
plot(sma200, color=color.orange, title="200 SMA")
plot(bbUpper, color=color.purple, title="Upper Bollinger Band")
plot(bbLower, color=color.purple, title="Lower Bollinger Band")

// --- Add Contextual Visuals ---
hline(70, "RSI Overbought", color=color.red)
hline(30, "RSI Oversold", color=color.green)
plot(rsiValue, color=color.blue, title="RSI")
plot(stochK, color=color.orange, title="Stochastic K")
plot(stochD, color=color.teal, title="Stochastic D")
plot(macdHist, color=color.gray, style=plot.style_histogram, title="MACD Histogram")

// --- Moving Averages Plot ---
plot(sma50, color=color.blue, linewidth=1, title="50-period SMA")
plot(sma200, color=color.orange, linewidth=1, title="200-period SMA")
plot(ema50, color=color.green, linewidth=1, title="50-period EMA")
plot(ema200, color=color.red, linewidth=1, title="200-period EMA")

// --- RSI Plot ---
hline(rsiOverbought, "Overbought", color=color.red)
hline(rsiOversold, "Oversold", color=color.green)
plot(rsiValue, color=color.blue, title="RSI")

// --- Stochastic RSI Plot ---
hline(stochOverbought, "Stochastic Overbought", color=color.red)
hline(stochOversold, "Stochastic Oversold", color=color.green)
plot(stochRSI, color=color.orange, title="Stochastic RSI")

// --- Bollinger Bands Plot ---
bbUpperPlot = plot(bbUpper, color=color.purple, linewidth=1, title="Upper Bollinger Band")
bbLowerPlot = plot(bbLower, color=color.purple, linewidth=1, title="Lower Bollinger Band")
fill(bbUpperPlot, bbLowerPlot, color=color.purple, title="Bollinger Bands Fill")

// --- Parabolic SAR Plot ---
plot(sar, color=color.blue, style=plot.style_cross, linewidth=2, title="Parabolic SAR")





//@version=6
// indicator("Comprehensive Buy/Sell Strategy with Advanced Indicators", overlay=true)

// // --- Candlestick Patterns ---
// bullishEngulfing = ta.candlepattern(ta.patterns.bullishengulfing)
// bearishEngulfing = ta.candlepattern(ta.patterns.bearishengulfing)
// bullishHammer = ta.candlepattern(ta.patterns.hammer)
// bearishHammer = ta.candlepattern(ta.patterns.invertedhammer)
// doji = ta.candlepattern(ta.patterns.doji)
// morningStar = ta.candlepattern(ta.patterns.morningstar)
// eveningStar = ta.candlepattern(ta.patterns.eveningstar)
// piercingLine = ta.candlepattern(ta.patterns.piercing)
// darkCloudCover = ta.candlepattern(ta.patterns.darkcloudcover)
// threeWhiteSoldiers = ta.candlepattern(ta.patterns.threewhitesoldiers)
// threeBlackCrows = ta.candlepattern(ta.patterns.threeblackcrows)
// engulfing = ta.candlepattern(ta.patterns.engulfing)
// abandonedBaby = ta.candlepattern(ta.patterns.abandonedbaby)
// shootingStar = ta.candlepattern(ta.patterns.shootingstar)
// hangingMan = ta.candlepattern(ta.patterns.hangingman)
// gravestoneDoji = ta.candlepattern(ta.patterns.gravestonedoji)
// dragonflyDoji = ta.candlepattern(ta.patterns.dragonflydoji)
// marubozu = ta.candlepattern(ta.patterns.marubozu)

// // --- Moving Averages ---
// smaShort = ta.sma(close, 50)
// smaLong = ta.sma(close, 200)
// emaShort = ta.ema(close, 50)
// emaLong = ta.ema(close, 200)

// // --- RSI ---
// rsiPeriod = 14
// rsiValue = ta.rsi(close, rsiPeriod)
// rsiOverbought = 70
// rsiOversold = 30

// // --- Stochastic RSI ---
// stochRSI = ta.stochrsi(close, 14)
// stochOverbought = 0.8
// stochOversold = 0.2

// // --- MACD ---
// [macdLine, signalLine, _] = ta.macd(close, 12, 26, 9)
// macdHist = macdLine - signalLine

// // --- Bollinger Bands ---
// bbPeriod = 20
// bbDev = 2.0
// basis = ta.sma(close, bbPeriod)
// bbUpper = basis + bbDev * ta.stdev(close, bbPeriod)
// bbLower = basis - bbDev * ta.stdev(close, bbPeriod)

// // --- Parabolic SAR ---
// sar = ta.sar(0.02, 0.2)

// // --- Volume Analysis ---
// volMA = ta.sma(volume, 20)
// highVolume = volume > volMA

// // --- Buy and Sell Conditions ---
// buySignal = bullishEngulfing or bullishHammer or doji or morningStar or piercingLine or threeWhiteSoldiers or engulfing or (emaShort > emaLong and macdHist > 0 and rsiValue < rsiOversold and close < bbLower and stochRSI < stochOversold and sar < close)
// sellSignal = bearishEngulfing or bearishHammer or eveningStar or darkCloudCover or threeBlackCrows or shootingStar or hangingMan or gravestoneDoji or dragonflyDoji or marubozu or (emaShort < emaLong and macdHist < 0 and rsiValue > rsiOverbought and close > bbUpper and stochRSI > stochOverbought and sar > close)

// // --- Plot Buy and Sell Signals ---
// plotshape(series=buySignal, location=location.belowbar, color=color.green, style=shape.labelup, title="Buy Signal", text="BUY")
// plotshape(series=sellSignal, location=location.abovebar, color=color.red, style=shape.labeldown, title="Sell Signal", text="SELL")

// // --- Moving Averages Plot ---
// plot(smaShort, color=color.blue, linewidth=1, title="50-period SMA")
// plot(smaLong, color=color.orange, linewidth=1, title="200-period SMA")
// plot(emaShort, color=color.green, linewidth=1, title="50-period EMA")
// plot(emaLong, color=color.red, linewidth=1, title="200-period EMA")

// // --- RSI Plot ---
// hline(rsiOverbought, "Overbought", color=color.red)
// hline(rsiOversold, "Oversold", color=color.green)
// plot(rsiValue, color=color.blue, title="RSI")

// // --- Stochastic RSI Plot ---
// hline(stochOverbought, "Stochastic Overbought", color=color.red)
// hline(stochOversold, "Stochastic Oversold", color=color.green)
// plot(stochRSI, color=color.orange, title="Stochastic RSI")

// // --- Bollinger Bands Plot ---
// plot(bbUpper, color=color.purple, linewidth=1, title="Upper Bollinger Band")
// plot(bbLower, color=color.purple, linewidth=1, title="Lower Bollinger Band")
// fill(bbUpper, bbLower, color=color.purple, transp=90, title="Bollinger Bands Fill")

// // --- Parabolic SAR Plot ---
// plot(sar, color=color.blue, style=plot.style_cross, linewidth=2, title="Parabolic SAR")






// //@version=5
// indicator("Comprehensive Buy/Sell Strategy with Advanced Indicators", overlay=true)

// // --- Candlestick Patterns ---
// bullishEngulfing = ta.candlepattern("bullishengulfing")
// bearishEngulfing = ta.candlepattern("bearishengulfing")
// bullishHammer = ta.candlepattern("hammer")
// bearishHammer = ta.candlepattern("invertedhammer")
// doji = ta.candlepattern("doji")
// morningStar = ta.candlepattern("morningstar")
// eveningStar = ta.candlepattern("eveningstar")
// piercingLine = ta.candlepattern("piercing")
// darkCloudCover = ta.candlepattern("darkcloudcover")
// threeWhiteSoldiers = ta.candlepattern("threewhitesoldiers")
// threeBlackCrows = ta.candlepattern("threeblackcrows")
// engulfing = ta.candlepattern("engulfing")
// abandonedBaby = ta.candlepattern("abandonedbaby")
// shootingStar = ta.candlepattern("shootingstar")
// hangingMan = ta.candlepattern("hangingman")
// gravestoneDoji = ta.candlepattern("gravestonedoji")
// dragonflyDoji = ta.candlepattern("dragonflydoji")
// marubozu = ta.candlepattern("marubozu")

// // --- Moving Averages ---
// smaShort = ta.sma(close, 50)
// smaLong = ta.sma(close, 200)
// emaShort = ta.ema(close, 50)
// emaLong = ta.ema(close, 200)

// // --- RSI ---
// rsiPeriod = 14
// rsiValue = ta.rsi(close, rsiPeriod)
// rsiOverbought = 70
// rsiOversold = 30

// // --- Stochastic RSI ---
// stochRSI = ta.stochrsi(close, 14)
// stochOverbought = 0.8
// stochOversold = 0.2

// // --- MACD ---
// [macdLine, signalLine, _] = ta.macd(close, 12, 26, 9)
// macdHist = macdLine - signalLine

// // --- Bollinger Bands ---
// bbPeriod = 20
// bbDev = 2.0
// basis = ta.sma(close, bbPeriod)
// bbUpper = basis + bbDev * ta.stdev(close, bbPeriod)
// bbLower = basis - bbDev * ta.stdev(close, bbPeriod)

// // --- Parabolic SAR ---
// sar = ta.sar(0.02, 0.2)

// // --- Volume Analysis ---
// volMA = ta.sma(volume, 20)
// highVolume = volume > volMA

// // --- Buy and Sell Conditions ---
// buySignal = bullishEngulfing or bullishHammer or doji or morningStar or piercingLine or threeWhiteSoldiers or engulfing or (emaShort > emaLong and macdHist > 0 and rsiValue < rsiOversold and close < bbLower and stochRSI < stochOversold and sar < close)
// sellSignal = bearishEngulfing or bearishHammer or eveningStar or darkCloudCover or threeBlackCrows or shootingStar or hangingMan or gravestoneDoji or dragonflyDoji or marubozu or (emaShort < emaLong and macdHist < 0 and rsiValue > rsiOverbought and close > bbUpper and stochRSI > stochOverbought and sar > close)

// // --- Plot Buy and Sell Signals ---
// plotshape(series=buySignal, location=location.belowbar, color=color.green, style=shape.labelup, title="Buy Signal", text="BUY")
// plotshape(series=sellSignal, location=location.abovebar, color=color.red, style=shape.labeldown, title="Sell Signal", text="SELL")

// // --- Moving Averages Plot ---
// plot(smaShort, color=color.blue, linewidth=1, title="50-period SMA")
// plot(smaLong, color=color.orange, linewidth=1, title="200-period SMA")
// plot(emaShort, color=color.green, linewidth=1, title="50-period EMA")
// plot(emaLong, color=color.red, linewidth=1, title="200-period EMA")

// // --- RSI Plot ---
// hline(rsiOverbought, "Overbought", color=color.red)
// hline(rsiOversold, "Oversold", color=color.green)
// plot(rsiValue, color=color.blue, title="RSI")

// // --- Stochastic RSI Plot ---
// hline(stochOverbought, "Stochastic Overbought", color=color.red)
// hline(stochOversold, "Stochastic Oversold", color=color.green)
// plot(stochRSI, color=color.orange, title="Stochastic RSI")

// // --- Bollinger Bands Plot ---
// plot(bbUpper, color=color.purple, linewidth=1, title="Upper Bollinger Band")
// plot(bbLower, color=color.purple, linewidth=1, title="Lower Bollinger Band")
// fill(bbUpper, bbLower, color=color.purple, transp=90, title="Bollinger Bands Fill")

// // --- Parabolic SAR Plot ---
// plot(sar, color=color.blue, style=plot.style_cross, linewidth=2, title="Parabolic SAR")

