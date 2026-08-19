
# Phishing Email Sample - Microsoft 365 Spoof

## Indicators of Compromise (IOC)
- Sender Spoofing → bounce@micros0ft-verify.com
- SPF Authentication Failure → spf=fail
- DKIM Absent → dkim=none
- Typosquat Domain → micros0ft-verify.com
- Urgency / Social Engineering → "Password expires in 24 hours"
- Suspicious URL / Redirect → https://micros0ft-verify.com/o365/verify

## Full Email Content
Return-Path: <bounce@micros0ft-verify.com>
Delivered-To: analyst@infoseclabs.io
Received: from mx.infoseclabs.io ([10.0.0.1]) by mail.infoseclabs.io with LMTP id K7f2J9mR3E for <analyst@infoseclabs.io>; Mon, 15 Jan 2024 09:47:12 -0500
Received: from mail.micros0ft-verify.com ([103.224.182.251]) by mx.infoseclabs.io with ESMTPS id 7b3f2c0f3-a1b2-4c5d-8e9f-0123456789ab for <analyst@infoseclabs.io>; Mon, 15 Jan 2024 09:47:10 -0500
Received: from [192.168.1.105] (unknown [103.224.182.251]) by mail.micros0ft-verify.com (Postfix) with ESMTPA id A1B2C3D4E5 for <analyst@infoseclabs.io>; Mon, 15 Jan 2024 14:45:23 +0000
Authentication-Results: mx.infoseclabs.io; spf=fail (domain of micros0ft-verify.com does not designate 103.224.182.251 as permitted sender) smtp.mailfrom=micros0ft-verify.com; dkim=none (message not signed); dmarc=fail (p=REJECT sp=REJECT) header.from=micros0ft-verify.com
From: "Microsoft 365 Team" <no-reply@micros0ft-verify.com>
Reply-To: account-verify@webmail-support.net
To: analyst@infoseclabs.io
Subject: Action Required: Your Microsoft 365 password expires in 24 hours
Date: Mon, 15 Jan 2024 14:45:23 +0000
Message-ID: <20240115094523.a1b2c3d4e5f6@micros0ft-verify.com>
MIME-Version: 1.0
Content-Type: multipart/alternative; boundary="----=_NextPart_000_001B_01D9F3A4.B5C6D7E8"
X-Mailer: PHPMailer 6.8.0
X-Priority: 1

------=_NextPart_000_001B_01D9F3A4.B5C6D7E8
Content-Type: text/plain; charset="UTF-8"
Content-Transfer-Encoding: quoted-printable

Dear Microsoft 365 User,
Your password will expire in 24 hours. To avoid losing access to your account, please verify your credentials immediately.
Click here to keep your current password: https://micros0ft-verify.com/o365/verify?token=a1b2c3d4e5f67890
If you do not verify within 24 hours, your account will be suspended and you will need to contact your system administrator to regain access.
This is an automated message. Please do not reply to this email.
Best regards,
Microsoft 365 Security Team

------=_NextPart_000_001B_01D9F3A4.B5C6D7E8
Content-Type: text/html; charset="UTF-8"
Content-Transfer-Encoding: quoted-printable

<html><body style="font-family:Segoe UI,Arial,sans-serif;background:#f4f4f4;padding:20px;">
<div style="max-width:600px;margin:0 auto;background:#fff;border:1px solid #ddd;">
<div style="background:#0078d4;padding:20px;text-align:center;">
<span style="color:#fff;font-size:20px;font-weight:bold;">Microsoft 365</span>
</div>
<div style="padding:30px;">
<h2 style="color:#333;">Password Expiration Notice</h2>
<p>Your Microsoft 365 password will expire in <strong>24 hours</strong>.</p>
<p>To avoid losing access to your account, please verify your credentials immediately.</p>
<div style="text-align:center;margin:30px 0;">
<a href="https://micros0ft-verify.com/o365/verify?token=a1b2c3d4e5f67890" style="background:#0078d4;color:#fff;padding:12px 30px;text-decoration:none;border-radius:4px;">Keep Current Password</a>
</div>
<p style="color:#666;font-size:12px;">If you do not verify within 24 hours, your account will be suspended.</p>
</div></div></body></html>

------=_NextPart_000_001B_01D9F3A4.B5C6D7E8--
