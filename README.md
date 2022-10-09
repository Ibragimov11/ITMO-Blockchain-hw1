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
