using Microsoft.VisualBasic;
using System;
using System.Windows.Forms;

namespace SWD_Semestra_project_Oskar_Vanegas_
{

    public partial class SalesRegister : Form
    {
        double price = 0;

        public SalesRegister()
        {
            InitializeComponent();
        }

        private void SalesRegister_Load(object sender, EventArgs e)
        {

            lblPrice.Text = (0).ToString("c");
        }



        private void btnCancel_Click(object sender, EventArgs e)
        {
            cboProduct.Text = "(Select product)";
            cboPayment.Text = "(Select payment method)";
            txtAmount.Clear();
            lblPrice.Text = (0).ToString("c");
            cboProduct.Focus();
        }

        private void btnExit_Click(object sender, EventArgs e)
        {
            DialogResult r = MessageBox.Show("Are you sure? ", "Do you want to close the sale?",
            MessageBoxButtons.YesNo, MessageBoxIcon.Exclamation);

            if (r == DialogResult.Yes) this.Close();
        }

        private void lblPrice_Click(object sender, EventArgs e)
        {

        }

        private void cboProduct_SelectedIndexChanged(object sender, EventArgs e)
        {
            string product = cboProduct.Text;
            if (product.Equals("T-shirts")) price = 250;
            if (product.Equals("Pants")) price = 500;
            if (product.Equals("Caps")) price = 300;
            if (product.Equals("Shorts")) price = 450;
            if (product.Equals("Hoodies")) price = 600;
            if (product.Equals("Jackets")) price = 850;

            lblPrice.Text = price.ToString("c");
        }

        private void btnRegister_Click(object sender, EventArgs e)
        {
            /* Validation of a product */
            if (cboProduct.SelectedIndex == -1)
            {
                MessageBox.Show("Please select a product...!!!");
            }
            else if (!Information.IsNumeric(txtAmount.Text))
            {
                MessageBox.Show("Please write a number...!!!");
            }
            else if (cboPayment.SelectedIndex == -1)
            {
                MessageBox.Show("Please select a payment method...!!!");
            }
            else
            {
                /*  Save data */
                string product = cboProduct.Text;
                int amount = Convert.ToInt32(txtAmount.Text);
                string payment = cboPayment.Text;

                /* Process data */
                double subtotal = amount * price;

                double discount = 0, charge = 0;
                if (payment.Equals("Credit cart"))
                {
                    discount = 0.5 * subtotal;
                }
                else
                {
                    charge = 0 * subtotal;
                }

                /* Final product is the total of amount and price */
                double finalProduct = amount * price;


                /* Showing data */
                ListViewItem row = new ListViewItem(product);
                row.SubItems.Add(amount.ToString());
                row.SubItems.Add(charge.ToString("c"));
                row.SubItems.Add(payment);
                row.SubItems.Add(finalProduct.ToString("c"));

                productData.Items.Add(row);



                /* Clear the ComboBox */
                cboProduct.SelectedIndex = -1;
                txtAmount.Clear();
                cboPayment.SelectedIndex = -1;
                cboProduct.Focus();
            }
        }



        private void txtAmount_TextChanged(object sender, EventArgs e)
        {

        }

        private void lblTitle_Click(object sender, EventArgs e)
        {

        }

        private void salesGroup_Enter(object sender, EventArgs e)
        {

        }



        private void lblDate_Click(object sender, EventArgs e)
        {
            lblDate.Text = DateTime.Now.ToString("yyyy-MM-dd HH:mm:ss");
        }

        private void lblD_Click(object sender, EventArgs e)
        {

        }
    }
}


