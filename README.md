# Power Query Lint Sample for Microsoft Fabric Notebook

Example of using Power Query Lint API in Microsoft Fabric Notebook

This project provides a Microsoft Fabric Notebook example for linting Power Query (M language) code using the PQLint API. The notebook demonstrates how to integrate automated code quality analysis for Power Query expressions directly within your Fabric workspace.

## Features

- **Interactive Analysis**: Run Power Query lint analysis directly in Fabric notebooks
- **Comprehensive Coverage**: Analyzes Power Query M language expressions and transformations
- **Detailed Reporting**: Provides color-coded output with severity levels (Error, Warning, Info)
- **Secure Key Management**: Uses Azure Key Vault for secure API key storage
- **Fabric Integration**: Seamlessly works within Microsoft Fabric workspace environment

## Getting Started

Follow these steps to set up the Power Query lint analysis in your Microsoft Fabric environment.

### Prerequisites

- **Microsoft Fabric Workspace**: Access to a Fabric workspace with notebook creation permissions
- **PQLint API Subscription**: A valid subscription key for the PQLint API
- **Azure Key Vault**: An Azure Key Vault instance to securely store the API subscription key
- **Power Query Knowledge**: Basic understanding of Power Query M language and expressions

### Installation Process

#### Step 1: Import the Notebook

1. Navigate to your Microsoft Fabric workspace
2. Click **"Import""**
3. Click **"From this computer""**
4. Upload the `lint-example.ipynb` file from this repository
5. The notebook will be imported and ready for configuration

#### Step 2: Set Up Azure Key Vault

The notebook requires Azure Key Vault to securely store your PQLint API subscription key.

1. **Create or access an existing Azure Key Vault**:
   - Navigate to the Azure portal
   - Create a new Key Vault or use an existing one
   - Ensure your Fabric workspace has access permissions

2. **Create a secret for the subscription key**:
   - In your Key Vault, go to **Secrets**
   - Click **"+ Generate/Import"**
   - Name: `pqlint-subscription-key` (or your preferred name)
   - Value: Your PQLint API subscription key
   - Click **"Create"**

3. **Configure Key Vault access**:
   - Ensure your Fabric workspace managed identity has **"Key Vault Secrets User"** role
   - Or configure appropriate access policies for secret retrieval
   - If running in the browser ensure you have access to Key Vault secrets.

#### Step 3: Configure the Notebook

Open the imported `lint-example.ipynb` notebook and update the following configuration variables:

1. **Key Vault Address**: Set your Azure Key Vault URL
   ```python
   # Update this with your Key Vault URL
   key_vault_url = "https://your-keyvault-name.vault.azure.net/"
   ```

2. **Workspace ID**: Set your Fabric workspace ID
   ```python
   # Update this with your Fabric workspace ID
   workspace_id = "your-workspace-id-here"
   ```

3. **Secret Name**: Update if you used a different name for your Key Vault secret
   ```python
   # Update if you used a different secret name
   secret_name = "pqlint-subscription-key"
   ```

### Customizing the Analysis

You can customize the notebook for your specific needs:

- **Code Sources**: Modify to read Power Query code from various sources (e.g., more than one workspace, Azure DevOps, etc.)
- **Analysis Rules**: Configure which linitng rules to run.
- **Output Format**: Customize the display and export of analysis results

### Understanding Results

#### Severity Levels
- **Error (3)**: Critical issues that will cause failures or incorrect results
- **Warning (2)**: Best practice violations that should be addressed

#### Output Format
For each issue found, the notebook displays:
- Rule name and severity level
- Rule ID and category
- Detailed description of the issue
- Location information (line numbers, character positions)
- Suggested fixes or improvements

A summary of the results by dataset is provided at the end of the execution as well.

### Security Considerations

- **Key Vault Integration**: API keys are stored securely in Azure Key Vault
- **No Hardcoded Secrets**: All sensitive information is retrieved from secure storage
- **Access Control**: Leverages Azure RBAC for Key Vault access management

### Troubleshooting

#### Common Issues

1. **"Key Vault access denied"**:
   - Verify your Fabric workspace managed identity has proper Key Vault permissions
   - Check that the Key Vault URL is correct
   - Ensure the secret name matches what's configured in the notebook

2. **"Subscription key invalid"**:
   - Verify your PQLint API key is correct and active
   - Check that the secret value in Key Vault is properly set
   - Ensure your API subscription hasn't expired

3. **"Workspace ID not found"**:
   - Verify the workspace ID is correct
   - Check that you're running the notebook in the correct Fabric workspace

4. **"Module import failed"**:
   - Ensure all required Python packages are installed
   - Check that the Fabric environment has internet access for API calls

#### Getting Help

If you encounter issues:
1. Check the Azure portal for Key Vault access logs
2. Verify your PQLint API subscription status
3. Review Fabric workspace permissions and settings
4. Consult the PQLint API documentation for specific error codes

### Contributing

To contribute to this project:
1. Fork the repository
2. Make your changes
3. Test thoroughly in a Fabric environment
4. Submit a pull request with detailed description of changes

### License

This project is licensed under the terms specified in the LICENSE file.
