<script>
	import { setContext, onMount, afterUpdate } from "svelte";
	import Total from "./Total.svelte";
	import Nav from "./Nav.svelte";
	import List from "./List.svelte";
	import ExpenseForm from "./ExpenseForm.svelte";
	import Allow from "./Allow.svelte";
	import Modal from "./Modal.svelte";

	let expenses = [];
	let setName = "";
	let setAmount = null;
	let setId = null;
	let isFormOpen = false;

	$: isEditing = setId ? true : false;
	$: total = expenses.reduce((acc, curr) => {
		return (acc += curr.amount);
	}, 0);

	function showForm() {
		isFormOpen = true;
	}

	function hideForm() {
		isFormOpen = false;
		setName = "";
		setAmount = null;
		setId = null;
	}

	function removeExpense(id) {
		expenses = expenses.filter((item) => item.id !== id);
	}

	function clearExpenses() {
		expenses = [];
	}

	function addExpense({ name, amount }) {
		let expense = { id: Math.random() * Date.now(), name, amount };
		expenses = [expense, ...expenses];
	}

	function setModifiedExpense(id) {
		let expense = expenses.find((item) => item.id === id);

		setId = expense.id;
		setName = expense.name;
		setAmount = expense.amount;
		showForm();
	}

	function editExpense({ name, amount }) {
		expenses = expenses.map((item) => {
			return item.id === setId ? { ...item, name, amount } : { ...item };
		});
		setId = null;
		setAmount = null;
		setName = "";
	}

	setContext("remove", removeExpense);
	setContext("modify", setModifiedExpense);

	function setLocalStorage() {
		localStorage.setItem("expenses", JSON.stringify(expenses));
	}

	onMount(() => {
		expenses = localStorage.getItem("expenses")
			? JSON.parse(localStorage.getItem("expenses"))
			: [];
	});
	afterUpdate(() => {
		console.log("after update");
		setLocalStorage();
	});
</script>

<main class="content">
	<Nav {showForm} />

	<Allow title="Total Allowed" {total} />
	<Total title="Monthly Expenses" {total} />
	{#if isFormOpen}
		<Modal>
			<ExpenseForm
				name={setName}
				amount={setAmount}
				{addExpense}
				{editExpense}
				{isEditing}
				{hideForm}
			/>
		</Modal>
	{/if}
	<List {expenses} />
	<button type="button" class="btn" on:click={clearExpenses}>
		Clear Expenses
	</button>
</main>

<style>
	main {
		text-transform: capitalize;
		text-align: center;
		padding: 1em;
		max-width: 800px;
		margin: 0 auto;
	}
	button {
		background: black;
		color: ivory;
		border: 0;
		cursor: pointer;
		border-radius: 6px;
		padding: 8px 12px;
		font-weight: bold;
		box-shadow: 1px 2px 3px black;
	}
	::backdrop {
		background-color: ivory;
	}
	@media screen and (min-width: 600px) {
		main {
			max-width: none;
		}
		@media screen and (max-width: 900px) {
			main {
				float: none;
				width: 100%;
			}
		}
	}
</style>
