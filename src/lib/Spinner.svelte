<script></script>

<div class="spinner"></div>

<style>
.spinner {
	position: fixed;
	top: 40%;
	left: 50%;
	transform: translate(-50%, -50%);
	border: 8px solid #f3f3f3;
	border-radius: 50%;
	border-top: 8px solid var(--primary);
	width: 40px;
	height: 40px;
	-webkit-animation: spin 1s linear infinite; /* Safari */
	animation: spin 1s linear infinite;
}

/* Safari */
@-webkit-keyframes spin {
	0% { -webkit-transform: rotate(0deg); }
	100% { -webkit-transform: rotate(360deg); }
}

@keyframes spin {
	0% { transform: rotate(0deg); }
	100% { transform: rotate(360deg); }
}
</style>
