# Banking Management System

This project implements a **Banking Management System** using SQL Server, featuring database tables, triggers, and stored procedures. It manages account opening, transactions, and KYC approval workflows while maintaining referential integrity.

## Features

- **Account Management**: 
  - Add new account details with mandatory KYC checks.
  - Maintain account holder details and balances.
- **Transactions**:
  - Supports debit and credit operations.
  - Updates account balance dynamically with triggers.
- **KYC Workflow**:
  - Automates account creation in the `BANK` and `ACCOUNT_HOLDER_DETAILS` tables upon KYC approval.
- **Transaction Logs**:
  - Procedure to fetch transaction records within the last 4 months.

## Database Structure

### Tables
1. **ACCOUNT_OPENING_FORM**:
   - Stores account holder details during registration.
2. **BANK**:
   - Maintains account balance and type.
3. **ACCOUNT_HOLDER_DETAILS**:
   - Records personal details of account holders.
4. **TRANSACTION_DETAILS**:
   - Logs all transactions with amounts and types.

### Triggers
1. **TR_APPROVED_KYC**:
   - Inserts data into `BANK` and `ACCOUNT_HOLDER_DETAILS` when the KYC status is updated to 'APPROVED'.
2. **TR_TRANSACTION**:
   - Updates `CURRENT_BALANCE` in `BANK` after debit or credit operations.

### Stored Procedure
- **SP_LOG_TRANSACTION**:
  - Fetches transaction logs for the last 4 months.

## How to Use

1. **Setup Database**:
   - Execute the script to create the database and tables.
   - Populate `ACCOUNT_OPENING_FORM` with sample data using `INSERT` statements.

2. **Update KYC Status**:
   - Approve KYC by updating `ACCOUNT_OPENING_FORM`. The triggers will populate related tables.

3. **Perform Transactions**:
   - Add transaction records in `TRANSACTION_DETAILS`. The account balances will update automatically.

4. **View Logs**:
   - Execute `SP_LOG_TRANSACTION` to fetch recent transaction logs.

## Example Queries

- Insert New Account:
  ```sql
  INSERT INTO ACCOUNT_OPENING_FORM (ACCOUNT_TYPE, ACCOUNT_HOLDER_NAME, DOB, AADHAR_NUMBER, MOBILE_NUMBER, ACCOUNT_OPENING_BALANCE)
  VALUES ('SAVINGS', 'John Doe', '1990-01-01', '123456789012', '9876543210', 5000.00);
  
Approve KYC:

UPDATE ACCOUNT_OPENING_FORM
SET KYC_STATUS = 'APPROVED'
WHERE ACCOUNT_HOLDER_NAME = 'John Doe';

Log a Transaction:

INSERT INTO TRANSACTION_DETAILS (ACCOUNT_NUMBER, PAYMENT_TYPE, TRANSACTION_AMOUNT, DATE_OF_TRANSACTION)
VALUES (1000001, 'CREDIT', 2000.00, '2025-01-01');
Fetch Transaction Logs:

EXEC SP_LOG_TRANSACTION;

Sample Data
Sample records are provided for testing account creation, transaction updates, and stored procedure functionality.

Requirements
SQL Server Management Studio
Basic understanding of SQL
