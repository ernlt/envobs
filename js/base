jQuery(function($){

	$(window).load(function() {
		$("body").removeClass("preload");
	});

	$(".container").hide();
	$(".home").show();
	$(".formComment").hide();

	$('.creationsLink.disabled').click(function(e) {
		e.preventDefault();
		alert("click");
	});

	$(".homeCell:not(.creation)").click(function(){
		data = $(this).data("page");
		$(".homeTable").stop().slideUp(700);
		$(".container").hide();
		$(".container."+data).stop().slideDown(700);
		$("body").addClass("darken");
		$(".creationsLink").addClass("disabled");
	});

	$(".back").click(function(){
		$(".container").stop().slideUp(600);
		$(".homeTable").stop().slideDown(600);
		$("body").removeClass("darken");
		$(".creationsLink").removeClass("disabled");
	});

	$("#sendMessage").submit(function(e){
		e.preventDefault();
		$.ajax({
			"url":"server/sendMessage.php",
			"type":"POST",
			"data":$(this).serialize(),
			"dataType":"json",
			"success":function(json){
				$(".formComment").stop();
				$(".formComment").attr("class", "formComment "+json.color);
				$(".formComment").html(json.reponse);
				if(json.success==1){
					$(".reinit_input").val("");
				}else{
					$.ajax({
						"url":"server/tools/createCaptcha.php",
						"dataType":"html",
						"success":function(data){
							drawCaptcha();
							$(".captcha_input").val("");
						}
					});
				}
				$(".formComment").slideDown(500).delay(2000).slideUp(1000);
			}
		});
	});

	function drawCaptcha(){
		let captcha = document.getElementById("captcha");
		let c = captcha.getContext("2d");
		c.clearRect(0, 0, captcha.width, captcha.height);
		let capt = "";
		$.ajax({
			"url":"server/tools/printCaptcha.php",
			"dataType":"html",
			"success":function(data){
				capt = data;
				let capts = capt.split("");
				let fonts = ["Arial","Times New Roman", "Georgia", "Impact"];
				for(let i=0; i < capts.length; i++){
					let char = capts[i];
					let font = fonts[Math.floor(Math.random() * 4)];
					let size = Math.floor(Math.random() * 20)+45;
					c.font = size+"px "+font;
					c.fillStyle = "#1abc9c";
					c.fillText(char, 10+i*45, 100);
				}
			}
		});
	}

	drawCaptcha();
	$("#captcha").click(drawCaptcha);

});
