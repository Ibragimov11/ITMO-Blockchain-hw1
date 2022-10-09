## Task 1

```diff
diff --git a/contracts/MultiSigWallet.sol b/contracts/MultiSigWallet.sol
index 6a777f2..ae95e82 100644
--- a/contracts/MultiSigWallet.sol
+++ b/contracts/MultiSigWallet.sol
@@ -91,6 +91,11 @@ contract MultiSigWallet {
         _;
     }
 
+    modifier validValue(uint value) {
+        require(value <= 66 ether);
+        _;
+    }
+
     /// @dev Fallback function allows to deposit ether.
     function()
         payable
@@ -289,6 +294,7 @@ contract MultiSigWallet {
     function addTransaction(address destination, uint value, bytes data)
         internal
         notNull(destination)
+        validValue(value)
         returns (uint transactionId)
     {
         transactionId = transactionCount;
```

## Task 2

```diff
diff --git a/contracts/token/ERC20/ERC20.sol b/contracts/token/ERC20/ERC20.sol
index 492e2610..65aaa3ae 100644
--- a/contracts/token/ERC20/ERC20.sol
+++ b/contracts/token/ERC20/ERC20.sol
@@ -221,6 +221,7 @@ contract ERC20 is Context, IERC20, IERC20Metadata {
      *
      * - `from` cannot be the zero address.
      * - `to` cannot be the zero address.
+     * - It's not Saturday
      * - `from` must have a balance of at least `amount`.
      */
     function _transfer(
@@ -230,6 +231,7 @@ contract ERC20 is Context, IERC20, IERC20Metadata {
     ) internal virtual {
         require(from != address(0), "ERC20: transfer from the zero address");
         require(to != address(0), "ERC20: transfer to the zero address");
+        require((block.timestamp / 1 days + 3) % 7 != 5, "Token transfers are not available on Saturdays");
 
         _beforeTokenTransfer(from, to, amount);
```
