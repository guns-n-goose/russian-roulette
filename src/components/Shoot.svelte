<script>
	import {kill, bullets, earnings} from '../store.js';
    b = $bullets;
    roll = [];
    for (i = 1; i <= 6; i++) {
        if (b > 0){
            roll.push(1);
            b--;
            roll = roll;
        }
        else {
            roll.push(0);
            roll = roll;
        }
    }

    function shoot() {
        var idx = Math.floor(Math.random() * roll.length);
        if (roll[idx] == 1) {
            kill.set(1);
            earnings.set(0);
        }
        else {
            earnings.update(n => n + 100 * 1);
        }
    }
</script>

<div>
    Test
</div>

<style>
.stripe {
		border-radius: 40px;
		position: relative;
		font-size: 3em;
    	font-family: 'Shadows Into Light';
		right: 200px;
		height: 100px;
		width: 200px;
		border: 2px solid #000000;
		color: #000000;
		background-image: repeating-linear-gradient(90deg, 
			rgba(20, 25, 25, 0.6),
			rgba(25, 25, 25, 0.6) 10%, 
			#4c4c4c 10%, #4c4c4c 20%);
		background-size: 100%;
		transition: background 0.3s ease-in-out;
		}
	.stripe:hover {
		background-position: 150px;
		}

</style>
