<script>
	import axios from 'axios';
	import Navbar from './Navbar.svelte';
	const currency = {
		AED: { name: 'United Arab Emirates Dirham', symbol: 'AED' },
		AFN: { name: 'Afghan Afghani', symbol: 'AFN' },
		ALL: { name: 'Albanian Lek', symbol: 'ALL' },
		AMD: { name: 'Armenian Dram', symbol: 'AMD' },
		ANG: { name: 'Netherlands Antillean Guilder', symbol: 'ANG' },
		AOA: { name: 'Angolan Kwanza', symbol: 'AOA' },
		ARS: { name: 'Argentine Peso', symbol: 'ARS' },
		AUD: { name: 'Australian Dollar', symbol: 'A$' },
		AWG: { name: 'Aruban Florin', symbol: 'AWG' },
		AZN: { name: 'Azerbaijani Manat', symbol: 'AZN' },
		BAM: { name: 'Bosnia-Herzegovina Convertible Mark', symbol: 'BAM' },
		BBD: { name: 'Barbadian Dollar', symbol: 'BBD' },
		BDT: { name: 'Bangladeshi Taka', symbol: 'BDT' },
		BGN: { name: 'Bulgarian Lev', symbol: 'BGN' },
		BHD: { name: 'Bahraini Dinar', symbol: 'BHD' },
		BIF: { name: 'Burundian Franc', symbol: 'BIF' },
		BMD: { name: 'Bermudan Dollar', symbol: 'BMD' },
		BND: { name: 'Brunei Dollar', symbol: 'BND' },
		BOB: { name: 'Bolivian Boliviano', symbol: 'BOB' },
		BRL: { name: 'Brazilian Real', symbol: 'R$' },
		BSD: { name: 'Bahamian Dollar', symbol: 'BSD' },
		BTN: { name: 'Bhutanese Ngultrum', symbol: 'BTN' },
		BWP: { name: 'Botswanan Pula', symbol: 'BWP' },
		BYR: { name: 'Belarusian Ruble', symbol: 'BYR' },
		BZD: { name: 'Belize Dollar', symbol: 'BZD' },
		CAD: { name: 'Canadian Dollar', symbol: 'CA$' },
		CDF: { name: 'Congolese Franc', symbol: 'CDF' },
		CHF: { name: 'Swiss Franc', symbol: 'CHF' },
		CLF: { name: 'Chilean Unit of Account (UF)', symbol: 'CLF' },
		CLP: { name: 'Chilean Peso', symbol: 'CLP' },
		CNY: { name: 'Chinese Yuan', symbol: 'CN¥' },
		COP: { name: 'Colombian Peso', symbol: 'COP' },
		CRC: { name: 'Costa Rican Colón', symbol: 'CRC' },
		CUC: { name: 'Cuban Convertible Peso', symbol: 'CUC' },
		CUP: { name: 'Cuban Peso', symbol: 'CUP' },
		CVE: { name: 'Cape Verdean Escudo', symbol: 'CVE' },
		CZK: { name: 'Czech Republic Koruna', symbol: 'CZK' },
		DJF: { name: 'Djiboutian Franc', symbol: 'DJF' },
		DKK: { name: 'Danish Krone', symbol: 'DKK' },
		DOP: { name: 'Dominican Peso', symbol: 'DOP' },
		DZD: { name: 'Algerian Dinar', symbol: 'DZD' },
		EGP: { name: 'Egyptian Pound', symbol: 'EGP' },
		ERN: { name: 'Eritrean Nakfa', symbol: 'ERN' },
		ETB: { name: 'Ethiopian Birr', symbol: 'ETB' },
		EUR: { name: 'Euro', symbol: '€' },
		FJD: { name: 'Fijian Dollar', symbol: 'FJD' },
		FKP: { name: 'Falkland Islands Pound', symbol: 'FKP' },
		GBP: { name: 'British Pound Sterling', symbol: '£' },
		GEL: { name: 'Georgian Lari', symbol: 'GEL' },
		GHS: { name: 'Ghanaian Cedi', symbol: 'GHS' },
		GIP: { name: 'Gibraltar Pound', symbol: 'GIP' },
		GMD: { name: 'Gambian Dalasi', symbol: 'GMD' },
		GNF: { name: 'Guinean Franc', symbol: 'GNF' },
		GTQ: { name: 'Guatemalan Quetzal', symbol: 'GTQ' },
		GYD: { name: 'Guyanaese Dollar', symbol: 'GYD' },
		HKD: { name: 'Hong Kong Dollar', symbol: 'HK$' },
		HNL: { name: 'Honduran Lempira', symbol: 'HNL' },
		HRK: { name: 'Croatian Kuna', symbol: 'HRK' },
		HTG: { name: 'Haitian Gourde', symbol: 'HTG' },
		HUF: { name: 'Hungarian Forint', symbol: 'HUF' },
		IDR: { name: 'Indonesian Rupiah', symbol: 'IDR' },
		ILP: { name: 'Israeli Pound', symbol: 'ILP' },
		ILS: { name: 'Israeli New Sheqel', symbol: '₪' },
		INR: { name: 'Indian Rupee', symbol: '₹' },
		IQD: { name: 'Iraqi Dinar', symbol: 'IQD' },
		IRR: { name: 'Iranian Rial', symbol: 'IRR' },
		ISK: { name: 'Icelandic Króna', symbol: 'ISK' },
		JMD: { name: 'Jamaican Dollar', symbol: 'JMD' },
		JOD: { name: 'Jordanian Dinar', symbol: 'JOD' },
		JPY: { name: 'Japanese Yen', symbol: '¥' },
		KES: { name: 'Kenyan Shilling', symbol: 'KES' },
		KGS: { name: 'Kyrgystani Som', symbol: 'KGS' },
		KHR: { name: 'Cambodian Riel', symbol: 'KHR' },
		KMF: { name: 'Comorian Franc', symbol: 'KMF' },
		KPW: { name: 'North Korean Won', symbol: 'KPW' },
		KRW: { name: 'South Korean Won', symbol: '₩' },
		KWD: { name: 'Kuwaiti Dinar', symbol: 'KWD' },
		KYD: { name: 'Cayman Islands Dollar', symbol: 'KYD' },
		KZT: { name: 'Kazakhstani Tenge', symbol: 'KZT' },
		LAK: { name: 'Laotian Kip', symbol: 'LAK' },
		LBP: { name: 'Lebanese Pound', symbol: 'LBP' },
		LKR: { name: 'Sri Lankan Rupee', symbol: 'LKR' },
		LRD: { name: 'Liberian Dollar', symbol: 'LRD' },
		LSL: { name: 'Lesotho Loti', symbol: 'LSL' },
		LVL: { name: 'Latvian Lats', symbol: 'LVL' },
		LYD: { name: 'Libyan Dinar', symbol: 'LYD' },
		MAD: { name: 'Moroccan Dirham', symbol: 'MAD' },
		MDL: { name: 'Moldovan Leu', symbol: 'MDL' },
		MGA: { name: 'Malagasy Ariary', symbol: 'MGA' },
		MKD: { name: 'Macedonian Denar', symbol: 'MKD' },
		MMK: { name: 'Myanmar Kyat', symbol: 'MMK' },
		MNT: { name: 'Mongolian Tugrik', symbol: 'MNT' },
		MOP: { name: 'Macanese Pataca', symbol: 'MOP' },
		MRO: { name: 'Mauritanian Ouguiya', symbol: 'MRO' },
		MUR: { name: 'Mauritian Rupee', symbol: 'MUR' },
		MVR: { name: 'Maldivian Rufiyaa', symbol: 'MVR' },
		MWK: { name: 'Malawian Kwacha', symbol: 'MWK' },
		MXN: { name: 'Mexican Peso', symbol: 'MX$' },
		MYR: { name: 'Malaysian Ringgit', symbol: 'MYR' },
		MZN: { name: 'Mozambican Metical', symbol: 'MZN' },
		NAD: { name: 'Namibian Dollar', symbol: 'NAD' },
		NGN: { name: 'Nigerian Naira', symbol: 'NGN' },
		NIO: { name: 'Nicaraguan Córdoba', symbol: 'NIO' },
		NOK: { name: 'Norwegian Krone', symbol: 'NOK' },
		NPR: { name: 'Nepalese Rupee', symbol: 'NPR' },
		NZD: { name: 'New Zealand Dollar', symbol: 'NZ$' },
		OMR: { name: 'Omani Rial', symbol: 'OMR' },
		PAB: { name: 'Panamanian Balboa', symbol: 'PAB' },
		PEN: { name: 'Peruvian Nuevo Sol', symbol: 'PEN' },
		PGK: { name: 'Papua New Guinean Kina', symbol: 'PGK' },
		PHP: { name: 'Philippine Peso', symbol: 'PHP' },
		PKR: { name: 'Pakistani Rupee', symbol: 'PKR' },
		PLN: { name: 'Polish Zloty', symbol: 'PLN' },
		PYG: { name: 'Paraguayan Guarani', symbol: 'PYG' },
		QAR: { name: 'Qatari Rial', symbol: 'QAR' },
		RON: { name: 'Romanian Leu', symbol: 'RON' },
		RSD: { name: 'Serbian Dinar', symbol: 'RSD' },
		RUB: { name: 'Russian Ruble', symbol: 'RUB' },
		RWF: { name: 'Rwandan Franc', symbol: 'RWF' },
		SAR: { name: 'Saudi Riyal', symbol: 'SAR' },
		SBD: { name: 'Solomon Islands Dollar', symbol: 'SBD' },
		SCR: { name: 'Seychellois Rupee', symbol: 'SCR' },
		SDG: { name: 'Sudanese Pound', symbol: 'SDG' },
		SEK: { name: 'Swedish Krona', symbol: 'SEK' },
		SGD: { name: 'Singapore Dollar', symbol: 'SGD' },
		SHP: { name: 'St. Helena Pound', symbol: 'SHP' },
		SLL: { name: 'Sierra Leonean Leone', symbol: 'SLL' },
		SOS: { name: 'Somali Shilling', symbol: 'SOS' },
		SRG: { name: 'Surinamese Guilder', symbol: 'SRG' },
		STD: { name: 'São Tomé & Príncipe Dobra', symbol: 'STD' },
		SVC: { name: 'Salvadoran Colón', symbol: 'SVC' },
		SYP: { name: 'Syrian Pound', symbol: 'SYP' },
		SZL: { name: 'Swazi Lilangeni', symbol: 'SZL' },
		THB: { name: 'Thai Baht', symbol: 'THB' },
		TJS: { name: 'Tajikistani Somoni', symbol: 'TJS' },
		TMT: { name: 'Turkmenistani Manat', symbol: 'TMT' },
		TND: { name: 'Tunisian Dinar', symbol: 'TND' },
		TOP: { name: 'Tongan Paʻanga', symbol: 'TOP' },
		TRY: { name: 'Turkish Lira', symbol: 'TRY' },
		TTD: { name: 'Trinidad & Tobago Dollar', symbol: 'TTD' },
		TWD: { name: 'New Taiwan Dollar', symbol: 'NT$' },
		TZS: { name: 'Tanzanian Shilling', symbol: 'TZS' },
		UAH: { name: 'Ukrainian Hryvnia', symbol: 'UAH' },
		UGX: { name: 'Ugandan Shilling', symbol: 'UGX' },
		USD: { name: 'US Dollar', symbol: '$' },
		UYU: { name: 'Uruguayan Peso', symbol: 'UYU' },
		UZS: { name: 'Uzbekistan Som', symbol: 'UZS' },
		VEF: { name: 'Venezuelan Bolívar', symbol: 'VEF' },
		VND: { name: 'Vietnamese Dong', symbol: '₫' },
		VUV: { name: 'Vanuatu Vatu', symbol: 'VUV' },
		WST: { name: 'Samoan Tala', symbol: 'WST' },
		XAF: { name: 'CFA Franc BEAC', symbol: 'FCFA' },
		XAG: { name: 'Silver', symbol: 'XAG' },
		XCD: { name: 'East Caribbean Dollar', symbol: 'EC$' },
		XDR: { name: 'Special Drawing Rights', symbol: 'XDR' },
		XOF: { name: 'CFA Franc BCEAO', symbol: 'CFA' },
		XPF: { name: 'CFP Franc', symbol: 'CFPF' },
		YER: { name: 'Yemeni Rial', symbol: 'YER' },
		ZAR: { name: 'South African Rand', symbol: 'ZAR' },
		ZMK: { name: 'Zambian Kwacha (1968–2012)', symbol: 'ZMK' },
		ZMW: { name: 'Zambian Kwacha', symbol: 'ZMW' },
		ZWL: { name: 'Zimbabwean Dollar (2009)', symbol: 'ZWL' }
	};
	let currencyValue1 = 'USD';
	let currencyValue2 = 'EUR';
	let amountValue = '';
	let newValue = '';
	let amountSet = {};

	async function transCurrency() {
		const temp = currencyValue1;
		currencyValue1 = currencyValue2;
		currencyValue2 = temp;
		await getValues();
	}

	async function convertCurrency() {
		const apiKey = '0IM1OGs36No1KIg69Tg75G4IiT5UvWVe8UrDaRnI'; // API anahtarını buraya ekleyin
		const url = 'https://api.api-ninjas.com/v1/convertcurrency';
		const want = currencyValue2;
		const have = currencyValue1;
		const amount = amountValue;

		// Axios ile GET isteği gönderme
		await axios
			.get(url, {
				params: {
					want,
					have,
					amount
				},
				headers: {
					'X-Api-Key': apiKey
				}
			})
			.then((response) => {
				// İstek başarılıysa burası çalışır
				newValue = response.data.new_amount;
			})
			.catch((error) => {
				// İstek hatalıysa burası çalışır
				console.error('Hata: ', error);
			});
	}
	const currencyList = ['USD', 'EUR', 'GBP', 'JPY', 'CNY', 'CAD', 'AUD', 'HKD', 'SGD', 'SEK'];

	async function convertCurrencies() {
		const apiKey = '0IM1OGs36No1KIg69Tg75G4IiT5UvWVe8UrDaRnI';
		const url = 'https://api.api-ninjas.com/v1/convertcurrency';
		const amount = amountValue;

		for (let i = 0; i < currencyList.length; i++) {
			const have = currencyValue1;
			const want = currencyList[i];

			await axios
				.get(url, {
					params: {
						want,
						have,
						amount
					},
					headers: {
						'X-Api-Key': apiKey
					}
				})
				.then((response) => {
					// İstek başarılıysa burası çalışır
					//console.log(`Dönüşüm (${have} -> ${want}): ${response.data.new_amount}`);
					amountSet[want] = response.data.new_amount;
				})
				.catch((error) => {
					// İstek hatalıysa burası çalışır
					console.error(`Dönüşüm (${have} -> ${want}) hatası:`, error);
				});
		}
	}

	// Fonksiyonu çağırarak döngüyü başlatın
	async function getValues() {
		await convertCurrency();
		await convertCurrencies();
	}
</script>

<Navbar />
<br /><br /><br /><br />
<main>
	<div class="container">
		<div class="div-row">
			<select bind:value={currencyValue1} class="" id="selectOptions">
				{#each Object.keys(currency) as item}
					<option value={item}>{item}</option>
				{/each}
			</select>
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<!-- svelte-ignore a11y-no-static-element-interactions -->
			<i class="bi bi-arrow-left-right" on:click={transCurrency} />
			<select bind:value={currencyValue2} class="" id="selectOptions">
				{#each Object.keys(currency) as item}
					<option value={item}>{item}</option>
				{/each}
			</select>
		</div>
	</div>
	<div class="amount-div">
		<input type="tel" name="" id="" placeholder="Amount" bind:value={amountValue} />
		<br />
		<button on:click={getValues}>GET</button>
	</div>
	<h2>{amountValue} {currencyValue1} = { newValue } {currencyValue2}</h2>
	<div class="others">
		<ul>
			{#each Object.keys(amountSet) as indis}
			{#if amountValue > amountSet[indis]}
			<li style="color: red;">
				<span>
					<span>{amountValue}</span>
					<span>{currencyValue1}</span>
				</span>
				<span>
					<span>{amountSet[indis]}</span>
					<span>{indis}</span>
				</span>
			</li>			
			{/if}
			{#if  amountValue < amountSet[indis]}
			<li style="color: green;">
				<span>
					<span>{amountValue}</span>
					<span>{currencyValue1}</span>
				</span>
				<span>
					<span>{amountSet[indis]}</span>
					<span>{indis}</span>
				</span>
			</li>
			{/if}
			{#if  amountValue === amountSet[indis]}
			<li style="color: white;">
				<span>
					<span>{amountValue}</span>
					<span>{currencyValue1}</span>
				</span>
				<span>
					<span>{amountSet[indis]}</span>
					<span>{indis}</span>
				</span>
			</li>
			{/if}
				
			{/each}
		</ul>
	</div>
</main>

<style lang="sass">
    @import '../scss/index.scss';
</style>
