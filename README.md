# Personal-Use

<html lang="en">

<head>
    <style>
        .from,.to{
            width: 100px !important;
        }
        
        .span{
            width: 154px;
    display: inline-block;
        }
    </style>
</head>

    <body>
        
        <div>


            <div>
                <span class="span">Course Fee</span>
                <select class="from" id="sel1">
                </select>
                <input type="text" class="searchBox" id="oamount">
            </div>
            <div>
                <span class="span">Transportation Fee</span>
                <select class="from" id="sel1">
                </select>
                <input type="text" class="searchBox" id="oamount">
            </div>
            <div>
                <span class="span">Accomodation Fee</span>
                <select class="from" id="sel1">
                </select>
                <input type="text" class="searchBox" id="oamount">
            </div>
            <div>
                <span class="span">Air Ticket Fee</span>
                <select class="from" id="sel1">
                </select>
                <input type="text" class="searchBox" id="oamount">
            </div>
            <div>
                <span class="span">Total Cost Calculation</span>
                <select class="to" id="sel2">
                </select>
                 <span class="finalValue"></span>
            </div>
        </div>
    
    
    
    
        <script>
            fetch("https://api.exchangerate-api.com/v4/latest/INR").then((data) => data.json()).then((data) => {
                let currency = Object.keys(data.rates);
                currency.forEach((data) => {
                    $(".from,.to").append(`<option value=${data}>${data}</option>`);
                })
            });
    
    
            $(".to,.from,input").on("change click", function () {
                getResults();
            });
    
            function getResults() {
                fetch(`https://api.exchangerate-api.com/v4/latest/USD`)
                    .then(currency => {
                        return currency.json();
                    }).then(displayResults);
            }
    
            function displayResults(currency) {
                let arryofValue = document.querySelectorAll(".from");
                let total = 0;
                arryofValue.forEach((element) => {
                    let fromRate = currency.rates[element.value];
                    let toRate = currency.rates[$(".to").val()];
                    total += toRate / fromRate * $(element).next('input').val()
    
                })
    
                $('.finalValue').text(total.toFixed(2));
    
            }
    
    
        </script>
    </body>
</html>
