<script>
	let titles = ["#", "Coin", "Price", "Price Change", "24h Volume"];
	let coins = [];
	const loadCoins = async () => {
		const res = await fetch(
			"https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false"
		);
		const data = await res.json();
		console.log(data);
		coins = data;
	};

	loadCoins();
</script>

<div class="container">
	<div class="row">
		<h1>Tabla</h1>
		<table class="table table-dark">
			<thead>
				<tr>
					{#each titles as title}
						<th>{title}</th>
					{/each}
				</tr>
			</thead>
			<tbody>
				{#each coins as coin, i}
					<tr>
						<td class="text-muted">{i + 1}</td>
						<td>
							<img src={coin.image} alt={coin.name} style="width: 2rem;" class="img-fluid me-2">
							<span>
								{coin.name}
							</span>
							<span class="text-muted text-uppercase ms-2">
								{coin.symbol}
							</span>
						</td>
						<td>
							{coin.current_price}
						</td>
						<td>
							{coin.price_change_percentage_24h}
						</td>
						<td>
							{coin.total_volume}
						</td>
					</tr>
				{/each}
			</tbody>
		</table>
	</div>
</div>

<style>
</style>
