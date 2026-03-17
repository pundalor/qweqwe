public partial class MainWindow : Window
    {
        
        public List<Product> _products;
        public MainWindow()
        {
            var context = new PostgresContext();
            InitializeComponent();
            type_box_call();
            var product = context.Products.ToList();
            _products = product.ToList();
            DataContext = new { Products = product };
        }
        public void type_box_call()
        {
            var context = new PostgresContext();
            var type = context.Types.Select(x => x.TypeName).ToList();
            type.Add("все типы");
            type_box.ItemsSource = type;
        }
        private void search_box_KeyUp(object? sender, Avalonia.Input.KeyEventArgs e)
        {
            var context = new PostgresContext();
            var search_text = search_box.Text;
            var search_list = context.Products.Where(x => x.Name.Contains(search_text) || x.Descript.Contains(search_text)).ToList();
            product_list.ItemsSource = search_list;

        }

        private void name_box_SelectionChanged(object? sender, SelectionChangedEventArgs e)
        {
            var context = new PostgresContext();
            switch (name_box.SelectedIndex)
            {
                case 1:
                    var sort_products = _products.OrderBy(x => x.Name);
                    product_list.ItemsSource = sort_products;
                    break;
                case 0:
                    product_list.ItemsSource = _products;
                    break;
                case 2:
                    sort_products = _products.OrderByDescending(x => x.Name);
                    product_list.ItemsSource = sort_products;
                    break;
            }
        }

        private void cost_box_SelectionChanged(object? sender, SelectionChangedEventArgs e)
        {
            switch (cost_box.SelectedIndex)
            {
                case 1:
                    var sort_products = _products.OrderBy(x => x.Cost);
                    product_list.ItemsSource = sort_products;
                    break;
                case 0:
                    product_list.ItemsSource = _products;
                    break;
                case 2:
                    sort_products = _products.OrderByDescending(x => x.Cost);
                    product_list.ItemsSource = sort_products;
                    break;
            }
        }

        private void type_box_SelectionChanged(object? sender, SelectionChangedEventArgs e)
        {
            var context = new PostgresContext();
            var select = type_box.SelectionBoxItem.ToString();
            if (select == "все типы")
            {
                product_list.ItemsSource = _products;
            }
            else
            {
                var sort = _products.Where(x => x.TypeId == context.Types.Where(x => x.TypeName == select).Select(x => x.Id).FirstOrDefault()).ToList();
                product_list.ItemsSource = sort;
            }
        }
    }
}
