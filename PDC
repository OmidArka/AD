خیلی هم عالی! 😎 حالا برای تبدیل Additional Domain Controller (ADC) به Primary Domain Controller (PDC) باید مراحل زیر رو انجام بدی:
🚀 تبدیل ADC به PDC در ویندوز سرور
1️⃣ انتقال FSMO Roles به سرور جدید

FSMO (Flexible Single Master Operations) شامل ۵ تا نقش هست که باید به سرور جدید منتقل بشن.
✅ روش GUI (گرافیکی)

۱. روی سرور جدید لاگین کن.
۲. Run رو باز کن و دستور dsa.msc رو اجرا کن.
۳. در Active Directory Users and Computers، راست کلیک کن روی Domain و گزینه Operations Masters رو بزن.
۴. در هر ۳ تب (RID، PDC، Infrastructure) دکمه Change رو بزن و سرور جدید رو انتخاب کن.
۵. حالا Run رو باز کن و دستور mmc رو تایپ کن، بعدش:

    از منوی File گزینه Add/Remove Snap-in رو بزن.
    گزینه Active Directory Schema رو اضافه کن.
    روی Active Directory Schema راست کلیک کن و Change Active Directory Domain Controller رو بزن.
    سرور جدید رو انتخاب کن، بعدش روی Operations Master راست کلیک کن و Change رو بزن.

🔹 اینطوری تمام ۵ نقش FSMO به سرور جدید منتقل میشه. ✅
✅ روش PowerShell (سریع‌تر و دقیق‌تر)

برای انتقال تمام FSMO Roles این دستور رو روی سرور جدید اجرا کن:

Move-ADDirectoryServerOperationMasterRole -Identity "FTP-1396" -OperationMasterRole 0,1,2,3,4 -Force

🔹 به جای "FTP-1396" اسم سرور جدید رو بزن.
🔹 اگر خواستی تک‌تک نقش‌ها رو جابجا کنی:

Move-ADDirectoryServerOperationMasterRole -Identity "FTP-1396" -OperationMasterRole PDCEmulator
Move-ADDirectoryServerOperationMasterRole -Identity "FTP-1396" -OperationMasterRole RIDMaster
Move-ADDirectoryServerOperationMasterRole -Identity "FTP-1396" -OperationMasterRole InfrastructureMaster
Move-ADDirectoryServerOperationMasterRole -Identity "FTP-1396" -OperationMasterRole SchemaMaster
Move-ADDirectoryServerOperationMasterRole -Identity "FTP-1396" -OperationMasterRole DomainNamingMaster

2️⃣ بررسی انتقال موفق FSMO Roles

بعد از انتقال، این دستور رو بزن تا مطمئن بشی:

netdom query fsmo

🔹 باید همه نقش‌ها روی سرور جدیدت نمایش داده بشن. ✅
3️⃣ حذف دامین کنترلر قدیمی (اختیاری)

اگر سرور قدیمی رو دیگه نمی‌خوای، باید demote کنی:
۱. Run رو باز کن و دستور dcpromo رو اجرا کن.
۲. گزینه Remove Active Directory Domain Services رو انتخاب کن.
۳. مراحل رو ادامه بده و سرور رو ری‌استارت کن.

📌 نکته:
اگر dcpromo کار نکرد، می‌تونی این دستور رو بزنی:

Uninstall-ADDSDomainController -DemoteOperationMasterRole -Force

4️⃣ آپدیت DNS و Global Catalog

۱. DNS رو روی سرور جدید تنظیم کن (ipconfig /flushdns و ipconfig /registerdns).
۲. Global Catalog رو روی سرور جدید فعال کن (dsa.msc → Properties → تیک Global Catalog).
۳. Replication رو بررسی کن:

repadmin /showrepl
repadmin /syncall /AePd

✅ حالا سرور جدید تبدیل به Primary Domain Controller شده! 🎉 🚀
You said:
Active Directory Schema این نیست توش
ChatGPT said:
ChatGPT

اگر "Active Directory Schema" در MMC نیست، باید اون رو فعال کنی.
✅ فعال‌سازی Active Directory Schema در MMC

۱. Run رو باز کن (Win + R) و اینو تایپ کن:

regsvr32 schmmgmt.dll

۲. روی OK کلیک کن. باید پیام "DllRegisterServer in schmmgmt.dll succeeded" ببینی.
✅ اضافه کردن Active Directory Schema به MMC

۱. Run رو باز کن و mmc تایپ کن، سپس Enter بزن.
2. در کنسول باز شده، به منوی File برو و Add/Remove Snap-in رو بزن.
3. در لیست Available snap-ins گزینه Active Directory Schema رو پیدا کن و Add بزن.
4. OK رو بزن تا اضافه بشه.

حالا می‌تونی Schema Master رو تغییر بدی. 🚀
