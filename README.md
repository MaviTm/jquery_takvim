# MaviTm Jquery Takvim Uygulaması

Haftanın ilk günü pazartesi olarak görüntüler. Başlangıç, bitiş yılları ayarlanabilinir, İstenirse geçmiş tarihleri seçimden kaldırılabilinir.

## v1.5 - Yeni Özellikler
> **Yeni eklenen tetikleyicier:** Ayarlarda onceUygula ve sonraUygula isimlerinde iki farklı tetikleyici eklendi. onceUygula metodu tanimlanirsa takvim govdesi olusmadan calisan ve this ile degiskenlere ulasir set veya get edebilirsiniz. Metoda parametre eklerseniz this haricinde  aktif olan inputa bu parametre ile erişebilirsiniz. this sadece sınıf degiskenlerini sunar. sonraUygula ayni onceUygula mantığı ile aynı düzende çalışır ve inputa gun bilgisi yazıldıktan sonra işlem yapar

## Örnekler
> **Haftanın 1., 3., 5. ve 7. günlerini engellemek için:** 

```javascript
$('.date').mavitmTakvim({
           baslangicYil:2005,
           bitisYil:2035,
           oncesiSecme:false,
        	 engelliHaftaGun:'1,3,5,7'
    	  });
```

> **Giriş ve çıkış tarihi ile ilgili bir ilişki örneği**

```javascript
$('.rdate').mavitmTakvim({
	baslangicYil:2005,
	bitisYil:2035,
	oncesiSecme:true,
	onceUygula: function(tag){
		if ($(tag).attr("id") == "checkout") {
			this._aktifDate = new Date();

			var dates = $("#checkin").val().split('/'); ////0-gun,1-ay,2-yil
			if(dates.length > 1) {
				var d = new Date(dates[1] + "/" + dates[0] + "/" + dates[2]);
				d.setDate(d.getDate() + 1);
				this._aktifDate = d;
			}
		} else {
			this._aktifDate = new Date();
		}
	},
	sonraUygula : function(tag){

		if($(tag).attr("id") == "checkin"){
			var eleman = $(tag);
			var kacGun = parseInt($(tag).attr("data-plusday"));
			if(!kacGun){kacGun = 1;}
			var dates = eleman.val().split('/'); ////0-gun,1-ay,2-yil
			var d = new Date(dates[1]+"/"+dates[0]+"/"+dates[2]);
			d.setDate(d.getDate()+kacGun);
			$("#checkout").val(d.getDate()+"/"+(d.getMonth() + 1)+"/"+ d.getFullYear());
		}

	}
});
```
