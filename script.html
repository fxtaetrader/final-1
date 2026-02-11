// ===== AUTHENTICATION & USER MANAGEMENT =====
const USERS_KEY = 'fxTaeUsers';
const CURRENT_USER_KEY = 'fxTaeCurrentUser';
const AUTH_KEY = 'fxTaeAuthenticated';
const TRADES_KEY = 'fxTaeTrades';
const GOALS_KEY = 'fxTaeGoals';
const TRANSACTIONS_KEY = 'fxTaeTransactions';
const TRADING_RULES_KEY = 'fxTaeTradingRules';
const STARTING_BALANCE_KEY = 'fxTaeStartingBalance';

// Initialize storage
function initializeStorage() {
    if (!localStorage.getItem(USERS_KEY)) {
        localStorage.setItem(USERS_KEY, JSON.stringify([]));
    }
    if (!localStorage.getItem(TRADES_KEY)) {
        localStorage.setItem(TRADES_KEY, JSON.stringify([]));
    }
    if (!localStorage.getItem(GOALS_KEY)) {
        localStorage.setItem(GOALS_KEY, JSON.stringify([]));
    }
    if (!localStorage.getItem(TRANSACTIONS_KEY)) {
        localStorage.setItem(TRANSACTIONS_KEY, JSON.stringify([]));
    }
    if (!localStorage.getItem(STARTING_BALANCE_KEY)) {
        localStorage.setItem(STARTING_BALANCE_KEY, '0');
    }
}

// ===== UTILITY FUNCTIONS =====
function formatCurrency(amount) {
    return new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD',
        minimumFractionDigits: 2,
        maximumFractionDigits: 2
    }).format(amount);
}

function formatCurrencyWithSign(amount) {
    const sign = amount >= 0 ? '+' : '-';
    return `${sign}${formatCurrency(Math.abs(amount))}`;
}

function formatDate(dateString) {
    return new Date(dateString).toLocaleDateString('en-US', {
        year: 'numeric',
        month: 'short',
        day: 'numeric'
    });
}

function formatDateTime(dateString, timeString) {
    return `${formatDate(dateString)} ${timeString}`;
}

function showToast(message, type = 'info') {
    const container = document.getElementById('toastContainer');
    if (!container) return;
    
    const toast = document.createElement('div');
    toast.className = `toast ${type}`;
    
    const iconMap = {
        'success': 'check-circle',
        'error': 'exclamation-circle',
        'warning': 'exclamation-triangle',
        'info': 'info-circle'
    };
    
    toast.innerHTML = `
        <i class="fas fa-${iconMap[type] || 'info-circle'}"></i>
        <span>${message}</span>
    `;
    
    container.appendChild(toast);
    
    setTimeout(() => {
        toast.remove();
    }, 3000);
}

// ===== DATA MANAGEMENT =====
let trades = [];
let goals = [];
let transactions = [];
let accountBalance = 0;
let startingBalance = 0;
let equityChart = null;
let winRateChart = null;
let winLossChart = null;
let winLossRatioChart = null;

function loadData() {
    try {
        trades = JSON.parse(localStorage.getItem(TRADES_KEY) || '[]');
        goals = JSON.parse(localStorage.getItem(GOALS_KEY) || '[]');
        transactions = JSON.parse(localStorage.getItem(TRANSACTIONS_KEY) || '[]');
        startingBalance = parseFloat(localStorage.getItem(STARTING_BALANCE_KEY) || '0');
        
        // Calculate current balance
        accountBalance = startingBalance;
        trades.forEach(trade => accountBalance += trade.pnl);
        transactions.forEach(transaction => {
            if (transaction.type === 'deposit') {
                accountBalance += transaction.amount;
            } else {
                accountBalance -= transaction.amount;
            }
        });
    } catch (error) {
        console.error('Error loading data:', error);
        trades = [];
        goals = [];
        transactions = [];
        accountBalance = 0;
        startingBalance = 0;
    }
}

function saveData() {
    try {
        localStorage.setItem(TRADES_KEY, JSON.stringify(trades));
        localStorage.setItem(GOALS_KEY, JSON.stringify(goals));
        localStorage.setItem(TRANSACTIONS_KEY, JSON.stringify(transactions));
        localStorage.setItem(STARTING_BALANCE_KEY, startingBalance.toString());
    } catch (error) {
        console.error('Error saving data:', error);
        showToast('Error saving data', 'error');
    }
}

// ===== DASHBOARD INITIALIZATION =====
function initializeDashboard() {
    if (!sessionStorage.getItem(AUTH_KEY)) {
        window.location.href = 'index.html';
        return;
    }
    
    initializeStorage();
    loadData();
    
    // Setup event listeners
    setupEventListeners();
    
    // Update all displays
    updateCurrentDate();
    updateUserInfo();
    updateAccountBalanceDisplay();
    updateStats();
    updateRecentActivity();
    updateTransactionsTable();
    updateAllTrades();
    updateGoalsList();
    
    // Set default dates
    const today = new Date().toISOString().split('T')[0];
    document.getElementById('tradeDate').value = today;
    document.getElementById('depositDate').value = today;
    document.getElementById('withdrawalDate').value = today;
    
    // Initialize charts
    setTimeout(() => {
        initializeCharts();
        updateCalendar();
    }, 500);
    
    // Set current time
    const now = new Date();
    const timeString = `${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}`;
    document.getElementById('tradeTime').value = timeString;
    document.getElementById('depositTime').value = timeString;
    document.getElementById('withdrawalTime').value = timeString;
    
    // Set theme
    const savedTheme = localStorage.getItem('fxTaeTheme') || 'light';
    setTheme(savedTheme);
    
    // Hide loader
    setTimeout(() => {
        const loader = document.getElementById('loader');
        const mainContainer = document.getElementById('mainContainer');
        if (loader && mainContainer) {
            loader.style.opacity = '0';
            setTimeout(() => {
                loader.style.display = 'none';
                mainContainer.style.display = 'block';
            }, 500);
        }
    }, 1000);
}

function updateCurrentDate() {
    const dateElement = document.getElementById('currentDate');
    if (dateElement) {
        dateElement.textContent = new Date().toLocaleDateString('en-US', {
            weekday: 'long',
            year: 'numeric',
            month: 'long',
            day: 'numeric'
        });
    }
}

function updateUserInfo() {
    const user = JSON.parse(localStorage.getItem(CURRENT_USER_KEY) || '{}');
    const userNameElement = document.getElementById('userName');
    const userEmailElement = document.getElementById('userEmail');
    const userEmailDisplay = document.getElementById('userEmailDisplay');
    
    if (userNameElement) userNameElement.textContent = user.name || 'Trader';
    if (userEmailElement) userEmailElement.textContent = user.email || 'trader@example.com';
    if (userEmailDisplay) userEmailDisplay.value = user.email || 'trader@example.com';
}

function updateAccountBalanceDisplay() {
    const balanceElement = document.getElementById('accountBalance');
    if (balanceElement) {
        balanceElement.textContent = formatCurrency(accountBalance);
    }
}

// ===== DEPOSIT & WITHDRAWAL FUNCTIONS =====
function updateBalanceCalculations() {
    const depositAmount = parseFloat(document.getElementById('depositAmount')?.value) || 0;
    const withdrawalAmount = parseFloat(document.getElementById('withdrawalAmount')?.value) || 0;
    
    const balanceAfterDeposit = document.getElementById('balanceAfterDeposit');
    const balanceAfterWithdrawal = document.getElementById('balanceAfterWithdrawal');
    
    if (balanceAfterDeposit) {
        balanceAfterDeposit.value = formatCurrency(accountBalance + depositAmount);
    }
    
    if (balanceAfterWithdrawal) {
        balanceAfterWithdrawal.value = formatCurrency(accountBalance - withdrawalAmount);
    }
}

function processDeposit() {
    try {
        const date = document.getElementById('depositDate').value;
        const time = document.getElementById('depositTime').value;
        const broker = document.getElementById('depositBroker').value;
        const amount = parseFloat(document.getElementById('depositAmount').value);
        const notes = document.getElementById('depositNotes').value;
        
        // Validation
        if (!date || !time || !broker || isNaN(amount) || amount <= 0) {
            showToast('Please fill all required fields with valid amounts', 'error');
            return false;
        }
        
        // Create transaction
        const transaction = {
            id: Date.now(),
            date,
            time,
            broker,
            amount,
            notes: notes || 'No notes provided',
            type: 'deposit',
            balanceBefore: accountBalance,
            balanceAfter: accountBalance + amount
        };
        
        // Update data
        transactions.unshift(transaction);
        accountBalance += amount;
        
        // Save and update
        saveData();
        updateAccountBalanceDisplay();
        updateRecentActivity();
        updateTransactionsTable();
        updateStats();
        
        // Update charts
        updateCharts();
        
        // Reset form
        document.getElementById('depositForm').reset();
        document.getElementById('depositDate').value = new Date().toISOString().split('T')[0];
        
        showToast(`Deposit of ${formatCurrency(amount)} processed successfully!`, 'success');
        return true;
    } catch (error) {
        console.error('Error processing deposit:', error);
        showToast('Error processing deposit', 'error');
        return false;
    }
}

function processWithdrawal() {
    try {
        const date = document.getElementById('withdrawalDate').value;
        const time = document.getElementById('withdrawalTime').value;
        const broker = document.getElementById('withdrawalBroker').value;
        const amount = parseFloat(document.getElementById('withdrawalAmount').value);
        const notes = document.getElementById('withdrawalNotes').value;
        
        // Validation
        if (!date || !time || !broker || isNaN(amount) || amount <= 0) {
            showToast('Please fill all required fields with valid amounts', 'error');
            return false;
        }
        
        if (amount > accountBalance) {
            showToast('Withdrawal amount exceeds account balance!', 'error');
            return false;
        }
        
        // Create transaction
        const transaction = {
            id: Date.now(),
            date,
            time,
            broker,
            amount,
            notes: notes || 'No notes provided',
            type: 'withdrawal',
            balanceBefore: accountBalance,
            balanceAfter: accountBalance - amount
        };
        
        // Update data
        transactions.unshift(transaction);
        accountBalance -= amount;
        
        // Save and update
        saveData();
        updateAccountBalanceDisplay();
        updateRecentActivity();
        updateTransactionsTable();
        updateStats();
        
        // Update charts
        updateCharts();
        
        // Reset form
        document.getElementById('withdrawalForm').reset();
        document.getElementById('withdrawalDate').value = new Date().toISOString().split('T')[0];
        
        showToast(`Withdrawal of ${formatCurrency(amount)} processed successfully!`, 'success');
        return true;
    } catch (error) {
        console.error('Error processing withdrawal:', error);
        showToast('Error processing withdrawal', 'error');
        return false;
    }
}

function saveAndDownloadDeposit() {
    if (processDeposit() && transactions.length > 0) {
        setTimeout(() => {
            downloadTransactionPDF(transactions[0]);
        }, 500);
    }
}

function saveAndDownloadWithdrawal() {
    if (processWithdrawal() && transactions.length > 0) {
        setTimeout(() => {
            downloadTransactionPDF(transactions[0]);
        }, 500);
    }
}

// ===== TRADE FUNCTIONS =====
function saveTrade() {
    try {
        const date = document.getElementById('tradeDate').value;
        const time = document.getElementById('tradeTime').value;
        const tradeNumber = parseInt(document.getElementById('tradeNumber').value);
        let strategy = document.getElementById('strategy').value;
        const customStrategy = document.getElementById('customStrategy').value;
        const pair = document.getElementById('currencyPair').value;
        const pnl = parseFloat(document.getElementById('pnlAmount').value);
        const notes = document.getElementById('tradeNotes').value;
        
        // Validation
        if (!date || !time || !tradeNumber || !strategy || !pair || isNaN(pnl)) {
            showToast('Please fill all required fields', 'error');
            return false;
        }
        
        // Check daily limit
        const todayTrades = trades.filter(t => t.date === date);
        if (todayTrades.length >= 4) {
            showToast('Maximum 4 trades per day reached!', 'error');
            return false;
        }
        
        // Use custom strategy if provided
        if (customStrategy && document.getElementById('customStrategy').style.display !== 'none') {
            strategy = customStrategy;
        }
        
        // Create trade
        const trade = {
            id: Date.now(),
            date,
            time,
            tradeNumber,
            pair,
            strategy,
            pnl,
            notes: notes || 'No notes provided',
            type: 'trade'
        };
        
        // Update data
        trades.unshift(trade);
        accountBalance += pnl;
        
        // Save and update
        saveData();
        updateAccountBalanceDisplay();
        updateRecentActivity();
        updateAllTrades();
        updateStats();
        
        // Update charts
        updateCharts();
        updateCalendar();
        
        // Reset form fields
        document.getElementById('pnlAmount').value = '';
        document.getElementById('tradeNotes').value = '';
        
        showToast('Trade saved successfully!', 'success');
        return true;
    } catch (error) {
        console.error('Error saving trade:', error);
        showToast('Error saving trade', 'error');
        return false;
    }
}

function saveAndDownloadTrade() {
    if (saveTrade() && trades.length > 0) {
        setTimeout(() => {
            downloadTradePDF(trades[0]);
        }, 500);
    }
}

// ===== UPDATE DISPLAYS =====
function updateStats() {
    const today = new Date().toISOString().split('T')[0];
    const todayTrades = trades.filter(t => t.date === today);
    const todayPnl = todayTrades.reduce((sum, t) => sum + t.pnl, 0);
    
    // Today's P&L
    const todayPnlElement = document.getElementById('todayPnl');
    if (todayPnlElement) {
        todayPnlElement.textContent = formatCurrencyWithSign(todayPnl);
        todayPnlElement.className = `stat-value ${todayPnl >= 0 ? 'profit' : 'loss'}`;
    }
    
    // Today's Trades Count
    const todayTradesCount = document.getElementById('todayTradesCount');
    if (todayTradesCount) {
        todayTradesCount.textContent = `${todayTrades.length}/4`;
    }
    
    // Progress bar
    const progressFill = document.querySelector('.progress-fill');
    if (progressFill) {
        progressFill.style.width = `${(todayTrades.length / 4) * 100}%`;
    }
    
    // Weekly stats
    const weekAgo = new Date(Date.now() - 7 * 86400000).toISOString().split('T')[0];
    const weeklyTrades = trades.filter(t => t.date >= weekAgo);
    const weeklyPnl = weeklyTrades.reduce((sum, t) => sum + t.pnl, 0);
    
    const weeklyPnlElement = document.getElementById('weeklyPnl');
    if (weeklyPnlElement) {
        weeklyPnlElement.textContent = formatCurrencyWithSign(weeklyPnl);
        weeklyPnlElement.className = `stat-value ${weeklyPnl >= 0 ? 'profit' : 'loss'}`;
    }
    
    // Monthly stats
    const monthAgo = new Date(Date.now() - 30 * 86400000).toISOString().split('T')[0];
    const monthlyTrades = trades.filter(t => t.date >= monthAgo);
    const monthlyPnl = monthlyTrades.reduce((sum, t) => sum + t.pnl, 0);
    
    const monthlyPnlElement = document.getElementById('monthlyPnl');
    if (monthlyPnlElement) {
        monthlyPnlElement.textContent = formatCurrencyWithSign(monthlyPnl);
        monthlyPnlElement.className = `stat-value ${monthlyPnl >= 0 ? 'profit' : 'loss'}`;
    }
    
    // Update trade lists
    updateTradeLists();
    updateWinRate();
}

function updateTradeLists() {
    const today = new Date().toISOString().split('T')[0];
    const todayTrades = trades.filter(t => t.date === today);
    const weekAgo = new Date(Date.now() - 7 * 86400000).toISOString().split('T')[0];
    const weeklyTrades = trades.filter(t => t.date >= weekAgo);
    const monthAgo = new Date(Date.now() - 30 * 86400000).toISOString().split('T')[0];
    const monthlyTrades = trades.filter(t => t.date >= monthAgo);
    
    updateTradeList('todayTradesList', todayTrades);
    updateTradeList('weeklyTradesList', weeklyTrades);
    updateTradeList('monthlyTradesList', monthlyTrades);
}

function updateTradeList(elementId, tradeList) {
    const element = document.getElementById(elementId);
    if (!element) return;
    
    if (tradeList.length === 0) {
        element.innerHTML = '<p class="no-trades">No trades recorded</p>';
        return;
    }
    
    const list = tradeList.slice(0, 3).map(trade => `
        <div class="trade-item">
            <span>${formatDateTime(trade.date, trade.time)}</span>
            <span>${trade.pair}</span>
            <span class="${trade.pnl >= 0 ? 'profit' : 'loss'}">${formatCurrencyWithSign(trade.pnl)}</span>
        </div>
    `).join('');
    
    element.innerHTML = list;
}

function updateWinRate() {
    const winningTrades = trades.filter(t => t.pnl > 0).length;
    const losingTrades = trades.filter(t => t.pnl < 0).length;
    const totalTrades = winningTrades + losingTrades;
    const winRate = totalTrades > 0 ? (winningTrades / totalTrades) * 100 : 0;
    
    const winRateElement = document.getElementById('winRateValue');
    if (winRateElement) {
        winRateElement.textContent = `${winRate.toFixed(1)}%`;
    }
}

function updateRecentActivity() {
    const tableBody = document.getElementById('recentActivityTable');
    if (!tableBody) return;
    
    // Combine trades and transactions
    const allActivities = [
        ...trades.map(t => ({...t, activityType: 'trade'})),
        ...transactions.map(t => ({...t, activityType: t.type}))
    ].sort((a, b) => new Date(b.date + ' ' + b.time) - new Date(a.date + ' ' + a.time))
     .slice(0, 5);
    
    if (allActivities.length === 0) {
        tableBody.innerHTML = `
            <tr>
                <td colspan="6" class="no-activity">
                    <i class="fas fa-chart-line"></i>
                    <p>No activity recorded yet.</p>
                </td>
            </tr>
        `;
        return;
    }
    
    tableBody.innerHTML = allActivities.map(activity => {
        if (activity.activityType === 'trade') {
            return `
                <tr>
                    <td>${formatDateTime(activity.date, activity.time)}</td>
                    <td><span class="activity-type trade-type">Trade</span></td>
                    <td>${activity.pair} - ${activity.strategy}</td>
                    <td class="${activity.pnl >= 0 ? 'profit' : 'loss'}">${formatCurrencyWithSign(activity.pnl)}</td>
                    <td><span class="status-badge ${activity.pnl >= 0 ? 'profit' : 'loss'}">${activity.pnl >= 0 ? 'WIN' : 'LOSS'}</span></td>
                    <td>
                        <button class="action-btn delete-btn" onclick="deleteTrade(${activity.id})" title="Delete">
                            <i class="fas fa-trash"></i>
                        </button>
                    </td>
                </tr>
            `;
        } else if (activity.activityType === 'deposit') {
            return `
                <tr>
                    <td>${formatDateTime(activity.date, activity.time)}</td>
                    <td><span class="activity-type deposit-type">Deposit</span></td>
                    <td>${activity.broker}</td>
                    <td class="profit">${formatCurrencyWithSign(activity.amount)}</td>
                    <td><span class="status-badge profit">COMPLETED</span></td>
                    <td>
                        <button class="action-btn delete-btn" onclick="deleteTransaction(${activity.id})" title="Delete">
                            <i class="fas fa-trash"></i>
                        </button>
                    </td>
                </tr>
            `;
        } else {
            return `
                <tr>
                    <td>${formatDateTime(activity.date, activity.time)}</td>
                    <td><span class="activity-type withdrawal-type">Withdrawal</span></td>
                    <td>${activity.broker}</td>
                    <td class="loss">${formatCurrencyWithSign(activity.amount)}</td>
                    <td><span class="status-badge profit">COMPLETED</span></td>
                    <td>
                        <button class="action-btn delete-btn" onclick="deleteTransaction(${activity.id})" title="Delete">
                            <i class="fas fa-trash"></i>
                        </button>
                    </td>
                </tr>
            `;
        }
    }).join('');
}

function updateTransactionsTable() {
    const tableBody = document.getElementById('transactionsTable');
    if (!tableBody) return;
    
    if (transactions.length === 0) {
        tableBody.innerHTML = `
            <tr>
                <td colspan="8" class="no-transactions">
                    <i class="fas fa-money-bill-wave"></i>
                    <p>No transactions recorded yet.</p>
                </td>
            </tr>
        `;
        return;
    }
    
    tableBody.innerHTML = transactions.map(transaction => `
        <tr>
            <td>${formatDateTime(transaction.date, transaction.time)}</td>
            <td><span class="activity-type ${transaction.type === 'deposit' ? 'deposit-type' : 'withdrawal-type'}">${transaction.type === 'deposit' ? 'Deposit' : 'Withdrawal'}</span></td>
            <td>${transaction.broker}</td>
            <td class="${transaction.type === 'deposit' ? 'transaction-deposit' : 'transaction-withdrawal'}">${formatCurrencyWithSign(transaction.type === 'deposit' ? transaction.amount : -transaction.amount)}</td>
            <td>${formatCurrency(transaction.balanceBefore)}</td>
            <td>${formatCurrency(transaction.balanceAfter)}</td>
            <td>${transaction.notes || 'No notes'}</td>
            <td>
                <button class="action-btn delete-btn" onclick="deleteTransaction(${transaction.id})" title="Delete">
                    <i class="fas fa-trash"></i>
                </button>
            </td>
        </tr>
    `).join('');
}

function updateAllTrades() {
    const tableBody = document.getElementById('allTradesTable');
    if (!tableBody) return;
    
    if (trades.length === 0) {
        tableBody.innerHTML = `
            <tr>
                <td colspan="8" class="no-trades">
                    <i class="fas fa-chart-line"></i>
                    <p>No trades recorded yet.</p>
                </td>
            </tr>
        `;
        return;
    }
    
    tableBody.innerHTML = trades.map(trade => `
        <tr>
            <td>${formatDateTime(trade.date, trade.time)}</td>
            <td>${trade.tradeNumber}</td>
            <td>${trade.pair}</td>
            <td>${trade.strategy}</td>
            <td class="${trade.pnl >= 0 ? 'profit' : 'loss'}">${formatCurrencyWithSign(trade.pnl)}</td>
            <td>${trade.notes || 'No notes'}</td>
            <td><span class="status-badge ${trade.pnl >= 0 ? 'profit' : 'loss'}">${trade.pnl >= 0 ? 'WIN' : 'LOSS'}</span></td>
            <td>
                <button class="action-btn delete-btn" onclick="deleteTrade(${trade.id})" title="Delete">
                    <i class="fas fa-trash"></i>
                </button>
            </td>
        </tr>
    `).join('');
}

// ===== DELETE FUNCTIONS =====
function deleteTrade(tradeId) {
    if (!confirm('Are you sure you want to delete this trade?')) return;
    
    const tradeIndex = trades.findIndex(t => t.id === tradeId);
    if (tradeIndex === -1) return;
    
    const trade = trades[tradeIndex];
    trades.splice(tradeIndex, 1);
    accountBalance -= trade.pnl;
    
    saveData();
    updateAccountBalanceDisplay();
    updateRecentActivity();
    updateAllTrades();
    updateStats();
    updateCharts();
    updateCalendar();
    
    showToast('Trade deleted successfully!', 'success');
}

function deleteTransaction(transactionId) {
    if (!confirm('Are you sure you want to delete this transaction?')) return;
    
    const transactionIndex = transactions.findIndex(t => t.id === transactionId);
    if (transactionIndex === -1) return;
    
    const transaction = transactions[transactionIndex];
    transactions.splice(transactionIndex, 1);
    
    if (transaction.type === 'deposit') {
        accountBalance -= transaction.amount;
    } else {
        accountBalance += transaction.amount;
    }
    
    saveData();
    updateAccountBalanceDisplay();
    updateRecentActivity();
    updateTransactionsTable();
    updateStats();
    updateCharts();
    
    showToast('Transaction deleted successfully!', 'success');
}

// ===== CHART FUNCTIONS =====
function initializeCharts() {
    // Equity Chart
    const equityCtx = document.getElementById('equityChart');
    if (equityCtx) {
        equityChart = new Chart(equityCtx, {
            type: 'line',
            data: getEquityData('1m'),
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { display: false },
                    tooltip: {
                        mode: 'index',
                        intersect: false,
                        callbacks: {
                            label: function(context) {
                                return `Balance: ${formatCurrency(context.parsed.y)}`;
                            }
                        }
                    }
                },
                scales: {
                    y: {
                        beginAtZero: false,
                        ticks: {
                            callback: function(value) {
                                return formatCurrency(value);
                            }
                        },
                        title: {
                            display: true,
                            text: 'Account Balance'
                        }
                    },
                    x: {
                        title: {
                            display: true,
                            text: 'Date'
                        }
                    }
                }
            }
        });
    }
    
    // Win Rate Chart
    const winRateCtx = document.getElementById('winRateChart');
    if (winRateCtx) {
        winRateChart = new Chart(winRateCtx, {
            type: 'doughnut',
            data: getWinRateData(),
            options: {
                responsive: true,
                maintainAspectRatio: false,
                cutout: '70%',
                plugins: {
                    legend: {
                        position: 'bottom',
                        labels: {
                            padding: 20,
                            usePointStyle: true,
                        }
                    }
                }
            }
        });
    }
    
    // Win Loss Chart
    const winLossCtx = document.getElementById('winLossChart');
    if (winLossCtx) {
        winLossChart = new Chart(winLossCtx, {
            type: 'pie',
            data: getWinLossData(),
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        position: 'bottom',
                        labels: {
                            padding: 20,
                            usePointStyle: true,
                        }
                    }
                }
            }
        });
    }
    
    // Win/Loss Ratio Chart
    const winLossRatioCtx = document.getElementById('winLossRatioChart');
    if (winLossRatioCtx) {
        winLossRatioChart = new Chart(winLossRatioCtx, {
            type: 'doughnut',
            data: getWinLossRatioData(),
            options: {
                responsive: true,
                maintainAspectRatio: false,
                cutout: '70%',
                circumference: 180,
                rotation: -90,
                plugins: {
                    legend: {
                        position: 'bottom',
                        labels: {
                            padding: 20,
                            usePointStyle: true,
                        }
                    }
                }
            }
        });
    }
}

function updateCharts() {
    if (equityChart) {
        const activePeriodBtn = document.querySelector('.period-btn.active');
        const period = activePeriodBtn ? activePeriodBtn.getAttribute('data-period') : '1m';
        equityChart.data = getEquityData(period);
        equityChart.update();
    }
    
    if (winRateChart) {
        winRateChart.data = getWinRateData();
        winRateChart.update();
    }
    
    if (winLossChart) {
        winLossChart.data = getWinLossData();
        winLossChart.update();
    }
    
    if (winLossRatioChart) {
        winLossRatioChart.data = getWinLossRatioData();
        winLossRatioChart.update();
    }
}

function getEquityData(period = '1m') {
    // Group all activities by date
    const activitiesByDate = {};
    
    // Add trades
    trades.forEach(trade => {
        const date = trade.date;
        if (!activitiesByDate[date]) {
            activitiesByDate[date] = 0;
        }
        activitiesByDate[date] += trade.pnl;
    });
    
    // Add transactions
    transactions.forEach(transaction => {
        const date = transaction.date;
        if (!activitiesByDate[date]) {
            activitiesByDate[date] = 0;
        }
        if (transaction.type === 'deposit') {
            activitiesByDate[date] += transaction.amount;
        } else {
            activitiesByDate[date] -= transaction.amount;
        }
    });
    
    let filteredDates = Object.keys(activitiesByDate);
    const now = new Date();
    
    // Filter based on period
    if (period === '12m') {
        // Get unique months with activity
        const monthsWithActivity = new Set();
        filteredDates.forEach(date => {
            const dateObj = new Date(date);
            const monthKey = `${dateObj.getFullYear()}-${dateObj.getMonth()}`;
            monthsWithActivity.add(monthKey);
        });
        
        // Create data for last 12 months with activity
        const monthlyData = [];
        for (let i = 11; i >= 0; i--) {
            const monthDate = new Date(now.getFullYear(), now.getMonth() - i, 1);
            const monthKey = `${monthDate.getFullYear()}-${monthDate.getMonth()}`;
            
            if (monthsWithActivity.has(monthKey)) {
                // Calculate net for this month
                const monthStart = new Date(monthDate.getFullYear(), monthDate.getMonth(), 1);
                const monthEnd = new Date(monthDate.getFullYear(), monthDate.getMonth() + 1, 0);
                
                let monthlyNet = 0;
                filteredDates.forEach(date => {
                    const dateObj = new Date(date);
                    if (dateObj >= monthStart && dateObj <= monthEnd) {
                        monthlyNet += activitiesByDate[date];
                    }
                });
                
                monthlyData.push({
                    date: monthDate,
                    net: monthlyNet,
                    label: monthDate.toLocaleDateString('en-US', { month: 'short', year: '2-digit' })
                });
            }
        }
        
        let balance = startingBalance;
        const data = [balance];
        const labels = ['Starting'];
        
        monthlyData.forEach(month => {
            balance += month.net;
            data.push(balance);
            labels.push(month.label);
        });
        
        return {
            labels: labels,
            datasets: [{
                label: 'Account Balance',
                data: data,
                borderColor: '#3b82f6',
                backgroundColor: 'rgba(59, 130, 246, 0.1)',
                borderWidth: 3,
                fill: true,
                tension: 0.4
            }]
        };
    } else {
        // 1 Month view
        const oneMonthAgo = new Date(now.setMonth(now.getMonth() - 1));
        filteredDates = filteredDates.filter(date => new Date(date) >= oneMonthAgo);
        
        filteredDates.sort((a, b) => new Date(a) - new Date(b));
        
        let balance = startingBalance;
        const data = [balance];
        const labels = ['Starting'];
        
        filteredDates.forEach(date => {
            const dailyNet = activitiesByDate[date];
            balance += dailyNet;
            data.push(balance);
            
            const dateObj = new Date(date);
            const formattedDate = dateObj.toLocaleDateString('en-US', {
                month: 'short',
                day: 'numeric'
            });
            labels.push(formattedDate);
        });
        
        if (filteredDates.length === 0) {
            return {
                labels: ['Starting Balance'],
                datasets: [{
                    label: 'Account Balance',
                    data: [startingBalance],
                    borderColor: '#3b82f6',
                    backgroundColor: 'rgba(59, 130, 246, 0.1)',
                    borderWidth: 3,
                    fill: true,
                    tension: 0.4
                }]
            };
        }
        
        return {
            labels: labels,
            datasets: [{
                label: 'Account Balance',
                data: data,
                borderColor: '#3b82f6',
                backgroundColor: 'rgba(59, 130, 246, 0.1)',
                borderWidth: 3,
                fill: true,
                tension: 0.4
            }]
        };
    }
}

function getWinRateData() {
    const winningTrades = trades.filter(t => t.pnl > 0).length;
    const losingTrades = trades.filter(t => t.pnl < 0).length;
    const breakEvenTrades = trades.filter(t => t.pnl === 0).length;
    
    return {
        labels: ['Winning Trades', 'Losing Trades', 'Break Even'],
        datasets: [{
            data: [winningTrades, losingTrades, breakEvenTrades],
            backgroundColor: ['#10b981', '#ef4444', '#94a3b8'],
            borderWidth: 0
        }]
    };
}

function getWinLossData() {
    const winningTrades = trades.filter(t => t.pnl > 0);
    const losingTrades = trades.filter(t => t.pnl < 0);
    
    const totalProfit = winningTrades.reduce((sum, t) => sum + t.pnl, 0);
    const totalLoss = Math.abs(losingTrades.reduce((sum, t) => sum + t.pnl, 0));
    
    return {
        labels: ['Total Profit', 'Total Loss'],
        datasets: [{
            data: [totalProfit, totalLoss],
            backgroundColor: ['#10b981', '#ef4444'],
            borderWidth: 0
        }]
    };
}

function getWinLossRatioData() {
    const winningTrades = trades.filter(t => t.pnl > 0).length;
    const losingTrades = trades.filter(t => t.pnl < 0).length;
    
    const winLossRatioElement = document.getElementById('winLossRatioValue');
    if (winLossRatioElement) {
        winLossRatioElement.textContent = `${winningTrades}:${losingTrades}`;
    }
    
    return {
        labels: ['Winning Trades', 'Losing Trades'],
        datasets: [{
            data: [winningTrades, losingTrades],
            backgroundColor: ['#10b981', '#ef4444'],
            borderWidth: 0
        }]
    };
}

// ===== CALENDAR FUNCTIONS =====
let currentCalendarMonth = new Date().getMonth();
let currentCalendarYear = new Date().getFullYear();

function updateCalendar() {
    const calendarGrid = document.getElementById('calendarGrid');
    const calendarMonth = document.getElementById('calendarMonth');
    
    if (!calendarGrid || !calendarMonth) return;
    
    const monthNames = ['January', 'February', 'March', 'April', 'May', 'June', 
                      'July', 'August', 'September', 'October', 'November', 'December'];
    calendarMonth.textContent = `${monthNames[currentCalendarMonth]} ${currentCalendarYear}`;
    
    const firstDay = new Date(currentCalendarYear, currentCalendarMonth, 1);
    const lastDay = new Date(currentCalendarYear, currentCalendarMonth + 1, 0);
    const daysInMonth = lastDay.getDate();
    const startingDay = firstDay.getDay();
    
    let calendarHTML = `
        <div class="calendar-header">Sun</div>
        <div class="calendar-header">Mon</div>
        <div class="calendar-header">Tue</div>
        <div class="calendar-header">Wed</div>
        <div class="calendar-header">Thu</div>
        <div class="calendar-header">Fri</div>
        <div class="calendar-header">Sat</div>
    `;
    
    for (let i = 0; i < startingDay; i++) {
        calendarHTML += '<div class="calendar-day empty"></div>';
    }
    
    for (let day = 1; day <= daysInMonth; day++) {
        const dateStr = `${currentCalendarYear}-${String(currentCalendarMonth + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
        const dayTrades = trades.filter(t => t.date === dateStr);
        const dayTransactions = transactions.filter(t => t.date === dateStr);
        
        let dayPnl = dayTrades.reduce((sum, t) => sum + t.pnl, 0);
        dayTransactions.forEach(t => {
            if (t.type === 'deposit') {
                dayPnl += t.amount;
            } else {
                dayPnl -= t.amount;
            }
        });
        
        let dayClass = 'calendar-day';
        let pnlClass = '';
        let pnlText = '';
        
        if (dayTrades.length > 0 || dayTransactions.length > 0) {
            dayClass += dayPnl >= 0 ? ' profit' : ' loss';
            pnlClass = dayPnl >= 0 ? 'profit' : 'loss';
            pnlText = formatCurrencyWithSign(dayPnl);
        }
        
        calendarHTML += `
            <div class="${dayClass}">
                <div class="calendar-date">${day}</div>
                ${(dayTrades.length > 0 || dayTransactions.length > 0) ? `
                    <div class="calendar-pnl ${pnlClass}">${pnlText}</div>
                    <div class="calendar-trades">${dayTrades.length + dayTransactions.length} activity</div>
                ` : ''}
            </div>
        `;
    }
    
    calendarGrid.innerHTML = calendarHTML;
}

function changeCalendarMonth(direction) {
    currentCalendarMonth += direction;
    
    if (currentCalendarMonth < 0) {
        currentCalendarMonth = 11;
        currentCalendarYear--;
    } else if (currentCalendarMonth > 11) {
        currentCalendarMonth = 0;
        currentCalendarYear++;
    }
    
    updateCalendar();
}

// ===== GOALS FUNCTIONS =====
function updateGoalsList() {
    const goalsList = document.getElementById('goalsList');
    if (!goalsList) return;
    
    if (goals.length === 0) {
        goalsList.innerHTML = `
            <div class="no-goals">
                <i class="fas fa-bullseye"></i>
                <p>No goals recorded yet. Write your first trading goal!</p>
            </div>
        `;
        return;
    }
    
    goalsList.innerHTML = goals.map(goal => `
        <div class="goal-card">
            <div class="goal-header">
                <span class="goal-date">${formatDate(goal.date)}</span>
                <div class="goal-actions">
                    <button class="action-btn delete-btn" onclick="deleteGoal(${goal.id})" title="Delete Goal">
                        <i class="fas fa-trash"></i>
                    </button>
                </div>
            </div>
            <div class="goal-content">${goal.content}</div>
        </div>
    `).join('');
}

function saveGoal() {
    const goalInput = document.getElementById('goalInput');
    const content = goalInput?.value.trim();
    
    if (!content) {
        showToast('Please write your goal first', 'error');
        return;
    }
    
    const goal = {
        id: Date.now(),
        date: new Date().toISOString().split('T')[0],
        content: content
    };
    
    goals.unshift(goal);
    saveData();
    updateGoalsList();
    
    if (goalInput) goalInput.value = '';
    showToast('Goal saved successfully!', 'success');
}

function clearGoal() {
    const goalInput = document.getElementById('goalInput');
    if (goalInput) goalInput.value = '';
}

function deleteGoal(goalId) {
    if (!confirm('Are you sure you want to delete this goal?')) return;
    
    goals = goals.filter(g => g.id !== goalId);
    saveData();
    updateGoalsList();
    
    showToast('Goal deleted successfully!', 'success');
}

// ===== SETTINGS FUNCTIONS =====
function setTheme(theme) {
    document.body.classList.toggle('dark-theme', theme === 'dark');
    localStorage.setItem('fxTaeTheme', theme);
    
    document.querySelectorAll('.theme-btn').forEach(btn => {
        btn.classList.toggle('active', 
            (theme === 'light' && btn.textContent.includes('Light')) || 
            (theme === 'dark' && btn.textContent.includes('Dark'))
        );
    });
    
    showToast(`Switched to ${theme} theme`, 'success');
}

function clearAllData() {
    if (!confirm('WARNING: This will delete ALL your data. This action cannot be undone. Are you sure?')) {
        return;
    }
    
    trades = [];
    goals = [];
    transactions = [];
    accountBalance = 0;
    startingBalance = 0;
    
    saveData();
    
    updateAccountBalanceDisplay();
    updateRecentActivity();
    updateTransactionsTable();
    updateAllTrades();
    updateGoalsList();
    updateStats();
    updateCharts();
    updateCalendar();
    
    showToast('All data cleared successfully!', 'success');
}

function saveUsername() {
    const newUsername = document.getElementById('editUsername')?.value.trim();
    
    if (!newUsername) {
        showToast('Please enter a username', 'error');
        return;
    }
    
    const user = JSON.parse(localStorage.getItem(CURRENT_USER_KEY) || '{}');
    user.name = newUsername;
    localStorage.setItem(CURRENT_USER_KEY, JSON.stringify(user));
    
    updateUserInfo();
    showToast('Username updated successfully!', 'success');
    
    document.getElementById('editUsername').value = '';
}

// ===== PDF EXPORT FUNCTIONS =====
function generatePDF({ title, content, filename }) {
    const { jsPDF } = window.jspdf;
    const pdf = new jsPDF();
    const pageWidth = pdf.internal.pageSize.width;
    const margin = 20;
    let yPosition = margin;
    
    pdf.setFontSize(24);
    pdf.setFont('helvetica', 'bold');
    pdf.setTextColor(59, 130, 246);
    pdf.text(title, margin, yPosition);
    yPosition += 15;
    
    pdf.setFontSize(12);
    pdf.setFont('helvetica', 'normal');
    pdf.setTextColor(100, 100, 100);
    pdf.text(`Generated: ${new Date().toLocaleDateString()}`, margin, yPosition);
    yPosition += 20;
    
    pdf.setDrawColor(200, 200, 200);
    pdf.line(margin, yPosition, pageWidth - margin, yPosition);
    yPosition += 10;
    
    pdf.setFontSize(11);
    pdf.setTextColor(0, 0, 0);
    
    const lines = pdf.splitTextToSize(content, pageWidth - 2 * margin);
    
    for (let i = 0; i < lines.length; i++) {
        if (yPosition > pdf.internal.pageSize.height - margin) {
            pdf.addPage();
            yPosition = margin;
        }
        pdf.text(lines[i], margin, yPosition);
        yPosition += 7;
    }
    
    pdf.save(filename);
    showToast(`PDF "${filename}" downloaded successfully!`, 'success');
}

function exportDepositsWithdrawalsPDF() {
    const deposits = transactions.filter(t => t.type === 'deposit');
    const withdrawals = transactions.filter(t => t.type === 'withdrawal');
    
    const content = `
        DEPOSITS & WITHDRAWALS REPORT
        
        Account Balance: ${formatCurrency(accountBalance)}
        Starting Balance: ${formatCurrency(startingBalance)}
        Net Growth: ${formatCurrency(accountBalance - startingBalance)}
        
        DEPOSITS (${deposits.length}):
        ${deposits.map(d => `
        ${formatDateTime(d.date, d.time)} | ${d.broker}
        Amount: ${formatCurrency(d.amount)}
        Notes: ${d.notes || 'No notes'}
        Balance: ${formatCurrency(d.balanceBefore)} → ${formatCurrency(d.balanceAfter)}
        `).join('\n')}
        
        WITHDRAWALS (${withdrawals.length}):
        ${withdrawals.map(w => `
        ${formatDateTime(w.date, w.time)} | ${w.broker}
        Amount: ${formatCurrency(w.amount)}
        Notes: ${w.notes || 'No notes'}
        Balance: ${formatCurrency(w.balanceBefore)} → ${formatCurrency(w.balanceAfter)}
        `).join('\n')}
        
        Total Deposited: ${formatCurrency(deposits.reduce((sum, d) => sum + d.amount, 0))}
        Total Withdrawn: ${formatCurrency(withdrawals.reduce((sum, w) => sum + w.amount, 0))}
    `;
    
    generatePDF({
        title: 'Deposits & Withdrawals Report',
        content: content,
        filename: `transactions-report-${new Date().toISOString().split('T')[0]}.pdf`
    });
}

function downloadTransactionPDF(transaction) {
    const content = `
        TRANSACTION RECEIPT
        
        Type: ${transaction.type === 'deposit' ? 'DEPOSIT' : 'WITHDRAWAL'}
        Date: ${formatDate(transaction.date)}
        Time: ${transaction.time}
        Transaction ID: ${transaction.id}
        Broker: ${transaction.broker}
        Amount: ${formatCurrency(transaction.amount)}
        
        Balance Before: ${formatCurrency(transaction.balanceBefore)}
        Balance After: ${formatCurrency(transaction.balanceAfter)}
        
        Notes: ${transaction.notes || 'No notes provided'}
        
        Generated: ${new Date().toLocaleDateString()} ${new Date().toLocaleTimeString()}
    `;
    
    generatePDF({
        title: `Transaction Receipt - ${transaction.type === 'deposit' ? 'Deposit' : 'Withdrawal'}`,
        content: content,
        filename: `transaction-${transaction.id}.pdf`
    });
}

// ===== EVENT LISTENERS =====
function setupEventListeners() {
    // Menu button
    const menuBtn = document.getElementById('menuBtn');
    const sidebar = document.getElementById('sidebar');
    
    if (menuBtn && sidebar) {
        menuBtn.addEventListener('click', () => {
            sidebar.classList.toggle('active');
        });
    }
    
    // Navigation items
    document.querySelectorAll('.nav-item').forEach(item => {
        item.addEventListener('click', function(e) {
            e.preventDefault();
            
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            this.classList.add('active');
            
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            
            const pageId = this.getAttribute('data-page');
            const pageElement = document.getElementById(pageId);
            if (pageElement) {
                pageElement.classList.add('active');
            }
            
            if (window.innerWidth <= 768 && sidebar) {
                sidebar.classList.remove('active');
            }
        });
    });
    
    // Period buttons
    document.querySelectorAll('.period-btn').forEach(btn => {
        btn.addEventListener('click', function() {
            document.querySelectorAll('.period-btn').forEach(b => b.classList.remove('active'));
            this.classList.add('active');
            
            if (equityChart) {
                const period = this.getAttribute('data-period');
                equityChart.data = getEquityData(period);
                equityChart.update();
            }
        });
    });
    
    // Logout button
    const logoutBtn = document.getElementById('logoutBtn');
    if (logoutBtn) {
        logoutBtn.addEventListener('click', function() {
            if (confirm('Are you sure you want to logout?')) {
                sessionStorage.removeItem(AUTH_KEY);
                localStorage.removeItem(CURRENT_USER_KEY);
                window.location.href = 'index.html';
            }
        });
    }
    
    // Deposit/Withdrawal amount inputs
    const depositAmountInput = document.getElementById('depositAmount');
    const withdrawalAmountInput = document.getElementById('withdrawalAmount');
    
    if (depositAmountInput) {
        depositAmountInput.addEventListener('input', updateBalanceCalculations);
    }
    
    if (withdrawalAmountInput) {
        withdrawalAmountInput.addEventListener('input', updateBalanceCalculations);
    }
}

// ===== INITIALIZE ON LOAD =====
document.addEventListener('DOMContentLoaded', function() {
    if (window.location.pathname.includes('dashboard.html')) {
        initializeDashboard();
    }
});
