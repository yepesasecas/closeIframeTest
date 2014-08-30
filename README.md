# [Close Iframe from inside using Server intermediary]
Close an Iframe using Hashes using a Server.

## Quick start

1.Copy the Javascript Hash Generator to your Source code
```
<script>
  function makehash(){var alpha="0123456789ABCDEF";var id='';for(var i=0;i<32;i++){id+=alpha.charAt(Math.round(Math.random()*14));}return id;}
  var IFRAME_HASH = makehash();
</script>
```

2. Generate a IFRAME_HASH with makehash()

3. Send the IFRAME_HASH as a Parameter to the POST. Url example:

```
"https://ztransaction.bongous.com/pay/xxx_newcheckout/?PARTNER_KEY=337dfc7f8aa28185ce1a6c44226c8ca4&TOTAL_DOMESTIC_SHIPPING_CHARGE=2.95&ORDER_CURRENCY=PEN&SHIP_COUNTRY=PE&PRODUCT_ID_1=12720644&PRODUCT_NAME_1=24/7 Comfort Apparel Women's Solid Sl&PRODUCT_PRICE_1=42.03&PRODUCT_Q_1=1&PRODUCT_TRANSIT_1=5&PRODUCT_DISTRIBUTION_COUNTRY_1=US&CUSTOM_ORDER_1=138522106&CUSTOM_ORDER_2=0.00&IFRAME_HASH=" + IFRAME_HASH 
```

4. before the `<iframe>` tag, copy and paste the next code. Remember to use IFRAME_HASH variable. 
```
<script>
  $(document).ready(function(){var BongoHideIframe={beURL:"http://ztransaction.bongous.com/static/partners/3301f/hash/"+"iframeStatus.php",checkStatus:function(){if($('#iframeLoader').is(':visible')){var dat={cmd:'checkStatus',iframe_hash:IFRAME_HASH};BongoTxRx.send(dat,this.beURL,{onSuccess:function(obj){if(obj.close==1){jBextend('#envoyContainer').hide();}}});}}};BongoHideIframe.checkStatus();setInterval(function(){BongoHideIframe.checkStatus();},10000);});
</script>
```

5. Now Test.