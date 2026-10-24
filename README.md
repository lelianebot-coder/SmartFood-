<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SmartFood — Еда для тех, кто ищет выгоду</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=Inter:wght@300;400;600;700&display=swap');

        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Inter', sans-serif; background: #faf8f5; color: #3a3a3a; line-height: 1.6; }
        h1, h2, h3, h4 { font-family: 'Playfair Display', serif; }

        /* HEADER */
        header {
            background: linear-gradient(135deg, #fff8f0 0%, #f5ebe0 100%);
            border-bottom: 3px solid #C75B39;
            padding: 15px 0;
            position: sticky;
            top: 0;
            z-index: 100;
            box-shadow: 0 2px 15px rgba(199,91,57,0.1);
        }
        .header-inner {
            max-width: 1200px; margin: 0 auto; padding: 0 20px;
            display: flex; justify-content: space-between; align-items: center; gap: 15px; flex-wrap: wrap;
        }
        .logo {
            font-size: 28px; font-weight: 900; color: #8B0000; text-decoration: none;
            display: flex; align-items: center; gap: 10px; font-family: 'Playfair Display', serif;
        }
        .logo-icon {
            width: 40px; height: 40px; background: linear-gradient(135deg, #C75B39, #8B0000);
            border-radius: 50%; display: flex; align-items: center; justify-content: center; color: white; font-size: 20px;
        }
        .logo span { color: #6B8E23; font-weight: 400; font-size: 14px; display: block; margin-top: -5px; font-family: 'Inter', sans-serif; }
        nav { display: flex; gap: 5px; flex-wrap: wrap; }
        nav button {
            background: transparent; border: 2px solid transparent; padding: 10px 20px; border-radius: 25px;
            cursor: pointer; font-size: 15px; font-weight: 600; color: #6b5a3e; transition: all 0.3s;
        }
        nav button:hover { background: #f5ebe0; color: #C75B39; }
        nav button.active { background: #C75B39; color: white; border-color: #C75B39; }
        .header-actions { display: flex; align-items: center; gap: 15px; }
        .date-display { background: #f5ebe0; padding: 8px 16px; border-radius: 20px; font-size: 13px; color: #8B0000; font-weight: 600; }
        .cart-btn {
            background: #C75B39; color: white; border: none; padding: 10px 20px; border-radius: 25px;
            cursor: pointer; font-size: 15px; font-weight: 600; position: relative; transition: all 0.3s;
        }
        .cart-btn:hover { background: #a84828; transform: scale(1.05); }
        .cart-count {
            position: absolute; top: -5px; right: -5px; background: #8B0000; color: white;
            width: 22px; height: 22px; border-radius: 50%; font-size: 12px; display: flex; align-items: center; justify-content: center; font-weight: 700;
        }

        /* HERO */
        .hero {
            background: linear-gradient(135deg, #fff8f0 0%, #f5ebe0 50%, #faf8f5 100%);
            padding: 60px 20px; text-align: center; position: relative; overflow: hidden;
        }
        .hero::before {
            content: ''; position: absolute; top: 0; left: 0; right: 0; bottom: 0;
            background-image: url('https://images.unsplash.com/photo-1509440159596-0249088772ff?w=1200&auto=format&fit=crop');
            background-size: cover; background-position: center; opacity: 0.08;
        }
        .hero-content { position: relative; z-index: 1; }
        .hero h1 { font-size: 48px; color: #3a3a3a; margin-bottom: 15px; font-weight: 900; }
        .hero h1 em { color: #C75B39; font-style: italic; }
        .hero p { font-size: 20px; color: #6b5a3e; max-width: 700px; margin: 0 auto 30px; font-style: italic; font-family: 'Playfair Display', serif; }
        .hero-stats { display: flex; justify-content: center; gap: 40px; flex-wrap: wrap; }
        .stat { text-align: center; }
        .stat-num { font-size: 36px; font-weight: 900; color: #C75B39; font-family: 'Playfair Display', serif; }
        .stat-label { font-size: 14px; color: #8b7a5e; }

        /* TABS */
        .tab-content { display: none; max-width: 1200px; margin: 0 auto; padding: 30px 20px; }
        .tab-content.active { display: block; animation: fadeIn 0.4s ease; }
        .section-title { font-size: 32px; color: #3a3a3a; margin-bottom: 10px; font-family: 'Playfair Display', serif; }
        .section-subtitle { color: #8b7a5e; margin-bottom: 30px; font-size: 16px; }

        /* FILTER */
        .filter-bar { display: flex; gap: 10px; margin-bottom: 25px; flex-wrap: wrap; align-items: center; }
        .filter-bar label { font-weight: 600; color: #6b5a3e; margin-right: 5px; }
        .filter-btn {
            background: white; border: 2px solid #f0e6d3; padding: 8px 18px; border-radius: 20px;
            cursor: pointer; font-size: 14px; color: #6b5a3e; transition: all 0.3s;
        }
        .filter-btn:hover, .filter-btn.active { background: #C75B39; color: white; border-color: #C75B39; }
        .search-box {
            margin-left: auto; padding: 10px 20px; border: 2px solid #f0e6d3; border-radius: 25px;
            font-size: 14px; width: 250px; outline: none; transition: border-color 0.3s;
        }
        .search-box:focus { border-color: #C75B39; }

        /* CARDS */
        .cards-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(340px, 1fr)); gap: 25px; }
        .place-card {
            background: white; border-radius: 16px; overflow: hidden; box-shadow: 0 4px 20px rgba(0,0,0,0.06);
            transition: all 0.3s; border: 1px solid #f0e6d3;
        }
        .place-card:hover { transform: translateY(-5px); box-shadow: 0 8px 30px rgba(199,91,57,0.2); }
        .card-image { height: 180px; background-size: cover; background-position: center; position: relative; }
        .card-image::after { content: ''; position: absolute; bottom: 0; left: 0; right: 0; height: 60px; background: linear-gradient(to top, rgba(0,0,0,0.3), transparent); }
        .card-header { background: linear-gradient(135deg, #f5ebe0, #fff8f0); padding: 20px; position: relative; }
        .card-header h3 { font-size: 22px; color: #3a3a3a; margin-bottom: 5px; font-family: 'Playfair Display', serif; }
        .card-type { display: inline-block; background: #C75B39; color: white; padding: 3px 12px; border-radius: 12px; font-size: 12px; font-weight: 600; }
        .card-distance { position: absolute; top: 15px; right: 15px; background: white; padding: 5px 12px; border-radius: 15px; font-size: 13px; font-weight: 600; color: #C75B39; }
        .card-body { padding: 20px; }
        .card-info { display: flex; flex-direction: column; gap: 8px; margin-bottom: 15px; }
        .card-info-row { display: flex; align-items: center; gap: 8px; font-size: 14px; color: #6b5a3e; }
        .card-info-row .icon { font-size: 16px; }
        .phone-row a { color: #C75B39; text-decoration: none; font-weight: 600; }
        .phone-row a:hover { text-decoration: underline; }
        .products-list { border-top: 1px solid #f0e6d3; padding-top: 15px; }
        .products-list h4 { font-size: 14px; color: #8b7a5e; margin-bottom: 10px; text-transform: uppercase; letter-spacing: 0.5px; }
        .product-item { display: flex; justify-content: space-between; align-items: flex-start; padding: 12px 0; border-bottom: 1px solid #faf8f5; gap: 10px; }
        .product-item:last-child { border-bottom: none; }
        .product-info-block { flex: 1; min-width: 0; }
        .product-name { font-size: 14px; color: #3a3a3a; font-weight: 600; margin-bottom: 3px; }
        .product-ingredients { font-size: 11px; color: #8b7a5e; margin-top: 4px; line-height: 1.4; font-style: italic; display: flex; align-items: flex-start; gap: 4px; }
        .product-ingredients .ing-icon { flex-shrink: 0; }
        .product-ingredients .ing-text { flex: 1; }
        .product-expiry { font-size: 11px; color: #8B0000; margin-top: 4px; font-weight: 600; }
        .product-prices { text-align: right; min-width: 100px; flex-shrink: 0; }
        .old-price { font-size: 13px; color: #aaa; text-decoration: line-through; }
        .new-price { font-size: 18px; font-weight: 800; color: #6B8E23; }
        .discount-badge { display: inline-block; background: #8B0000; color: white; padding: 2px 8px; border-radius: 8px; font-size: 11px; font-weight: 700; margin-top: 3px; }
        .add-btn { background: #C75B39; color: white; border: none; padding: 8px 16px; border-radius: 20px; cursor: pointer; font-size: 13px; font-weight: 600; transition: all 0.3s; margin-top: 5px; }
        .add-btn:hover { background: #a84828; transform: scale(1.05); }
        .add-btn.added { background: #6B8E23; }

        /* MAP */
        .map-container { background: white; border-radius: 16px; overflow: hidden; box-shadow: 0 4px 20px rgba(0,0,0,0.06); border: 1px solid #f0e6d3; }
        .map-placeholder {
            height: 500px; background: linear-gradient(135deg, #f5ebe0, #faf8f5); display: flex; align-items: center;
            justify-content: center; flex-direction: column; gap: 15px; position: relative;
            background-image: url('https://images.unsplash.com/photo-1524661135-423995f22d0b?w=1200&auto=format&fit=crop');
            background-size: cover; background-position: center;
        }
        .map-placeholder::before { content: ''; position: absolute; top: 0; left: 0; right: 0; bottom: 0; background: rgba(255,248,240,0.85); }
        .map-icon { font-size: 60px; position: relative; z-index: 1; }
        .map-title { font-size: 18px; color: #6b5a3e; font-weight: 600; position: relative; z-index: 1; }
        .map-subtitle { font-size: 14px; color: #8b7a5e; position: relative; z-index: 1; }
        .map-pin {
            position: absolute; background: #C75B39; color: white; width: 40px; height: 40px;
            border-radius: 50% 50% 50% 0; transform: rotate(-45deg); display: flex; align-items: center;
            justify-content: center; font-size: 16px; font-weight: 700; cursor: pointer; transition: all 0.3s;
            box-shadow: 0 3px 10px rgba(199,91,57,0.4); z-index: 2;
        }
        .map-pin:hover { transform: rotate(-45deg) scale(1.3); background: #8B0000; }
        .map-pin span { transform: rotate(45deg); }
        .map-legend { padding: 20px; display: flex; gap: 20px; flex-wrap: wrap; }
        .legend-item { display: flex; align-items: center; gap: 8px; font-size: 14px; color: #6b5a3e; }
        .legend-dot { width: 12px; height: 12px; border-radius: 50%; }

        /* HOW IT WORKS */
        .steps { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 25px; margin-top: 20px; }
        .step { background: white; border-radius: 16px; padding: 30px 20px; text-align: center; box-shadow: 0 4px 20px rgba(0,0,0,0.06); border: 1px solid #f0e6d3; }
        .step-num { width: 50px; height: 50px; background: #C75B39; color: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 22px; font-weight: 900; margin: 0 auto 15px; font-family: 'Playfair Display', serif; }
        .step h3 { font-size: 18px; color: #3a3a3a; margin-bottom: 8px; font-family: 'Playfair Display', serif; }
        .step p { font-size: 14px; color: #8b7a5e; }
        .step strong { color: #8B0000; }
        .benefits-block { margin-top: 40px; background: white; border-radius: 16px; padding: 30px; box-shadow: 0 4px 20px rgba(0,0,0,0.06); border: 1px solid #f0e6d3; }
        .benefits-title { font-size: 22px; color: #3a3a3a; margin-bottom: 15px; font-family: 'Playfair Display', serif; }
        .benefits-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; }
        .benefit-title { color: #C75B39; margin-bottom: 5px; }
        .benefit-text { font-size: 14px; color: #6b5a3e; }

        /* SAFETY */
        .safety-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 25px; }
        .safety-card { background: white; border-radius: 16px; padding: 30px; box-shadow: 0 4px 20px rgba(0,0,0,0.06); border: 1px solid #f0e6d3; }
        .safety-card .s-icon { font-size: 40px; margin-bottom: 15px; }
        .safety-card h3 { font-size: 20px; color: #3a3a3a; margin-bottom: 10px; font-family: 'Playfair Display', serif; }
        .safety-card p { font-size: 14px; color: #6b5a3e; line-height: 1.7; }
        .rating-stars { color: #f39c12; font-size: 18px; margin-top: 10px; }

        /* CHAT */
        .chat-container { background: white; border-radius: 16px; box-shadow: 0 4px 20px rgba(0,0,0,0.06); border: 1px solid #f0e6d3; overflow: hidden; max-width: 800px; margin: 0 auto; }
        .chat-header { background: linear-gradient(135deg, #C75B39, #8B0000); color: white; padding: 20px; display: flex; align-items: center; gap: 15px; }
        .chat-header-icon { width: 50px; height: 50px; background: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 24px; }
        .chat-header-info h3 { font-size: 20px; margin-bottom: 5px; }
        .chat-header-info p { font-size: 13px; opacity: 0.9; }
        .chat-status { width: 8px; height: 8px; background: #6B8E23; border-radius: 50%; display: inline-block; margin-right: 5px; animation: pulse 2s infinite; }
        .chat-messages { height: 400px; overflow-y: auto; padding: 20px; background: #faf8f5; display: flex; flex-direction: column; gap: 15px; }
        .chat-message { max-width: 70%; padding: 12px 16px; border-radius: 16px; font-size: 14px; line-height: 1.5; animation: fadeIn 0.3s ease; white-space: pre-wrap; }
        .chat-message.bot { background: white; border: 1px solid #f0e6d3; align-self: flex-start; border-bottom-left-radius: 4px; }
        .chat-message.user { background: #C75B39; color: white; align-self: flex-end; border-bottom-right-radius: 4px; }
        .chat-quick-replies { padding: 15px 20px; background: white; border-top: 1px solid #f0e6d3; display: flex; gap: 8px; flex-wrap: wrap; }
        .quick-reply { background: #f5ebe0; border: 1px solid #C75B39; color: #C75B39; padding: 8px 16px; border-radius: 20px; cursor: pointer; font-size: 13px; font-weight: 600; transition: all 0.3s; }
        .quick-reply:hover { background: #C75B39; color: white; }
        .chat-input-area { padding: 20px; background: white; border-top: 1px solid #f0e6d3; display: flex; gap: 10px; }
        .chat-input { flex: 1; padding: 12px 18px; border: 2px solid #f0e6d3; border-radius: 25px; font-size: 14px; outline: none; transition: border-color 0.3s; }
        .chat-input:focus { border-color: #C75B39; }
        .chat-send { background: #C75B39; color: white; border: none; padding: 12px 24px; border-radius: 25px; cursor: pointer; font-size: 14px; font-weight: 600; transition: all 0.3s; }
        .chat-send:hover { background: #a84828; }

        /* REVIEWS */
        .reviews-summary {
            background: white; border-radius: 16px; padding: 30px; box-shadow: 0 4px 20px rgba(0,0,0,0.06);
            border: 1px solid #f0e6d3; display: flex; gap: 40px; margin-bottom: 30px; flex-wrap: wrap; align-items: center;
        }
        .reviews-avg { text-align: center; min-width: 180px; }
        .reviews-avg-num { font-size: 56px; font-weight: 900; color: #C75B39; font-family: 'Playfair Display', serif; line-height: 1; }
        .reviews-avg-stars { color: #f39c12; font-size: 22px; margin: 8px 0; }
        .reviews-avg-count { font-size: 13px; color: #8b7a5e; }
        .reviews-bars { flex: 1; min-width: 280px; }
        .review-bar-row { display: flex; align-items: center; gap: 10px; margin-bottom: 6px; font-size: 13px; color: #6b5a3e; }
        .review-bar-row span:first-child { min-width: 35px; font-weight: 600; }
        .review-bar-row span:last-child { min-width: 35px; text-align: right; }
        .review-bar { flex: 1; height: 10px; background: #f5ebe0; border-radius: 5px; overflow: hidden; }
        .review-bar-fill { height: 100%; background: linear-gradient(90deg, #C75B39, #8B0000); border-radius: 5px; transition: width 1s ease; }
        .reviews-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 25px; }
        .review-card {
            background: white; border-radius: 16px; padding: 25px; box-shadow: 0 4px 20px rgba(0,0,0,0.06);
            border: 1px solid #f0e6d3; transition: all 0.3s;
        }
        .review-card:hover { transform: translateY(-3px); box-shadow: 0 8px 25px rgba(199,91,57,0.15); }
        .review-header { display: flex; align-items: center; gap: 12px; margin-bottom: 15px; }
        .review-avatar {
            width: 48px; height: 48px; border-radius: 50%; background: linear-gradient(135deg, #C75B39, #8B0000);
            color: white; display: flex; align-items: center; justify-content: center;
            font-size: 20px; font-weight: 700; font-family: 'Playfair Display', serif; flex-shrink: 0;
        }
        .review-author { flex: 1; }
        .review-author-name { font-size: 16px; font-weight: 700; color: #3a3a3a; font-family: 'Playfair Display', serif; }
        .review-author-role { font-size: 12px; color: #8b7a5e; margin-top: 2px; }
        .review-stars { color: #f39c12; font-size: 14px; }
        .review-text { font-size: 14px; color: #6b5a3e; line-height: 1.6; margin-bottom: 12px; font-style: italic; }
        .review-meta { display: flex; justify-content: space-between; align-items: center; font-size: 12px; color: #aaa; padding-top: 12px; border-top: 1px solid #f0e6d3; }
        .review-place { background: #f5ebe0; color: #C75B39; padding: 3px 10px; border-radius: 10px; font-size: 11px; font-weight: 600; }

        /* MODALS */
        .modal-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 1000; align-items: center; justify-content: center; }
        .modal-overlay.show { display: flex; }
        .modal { background: white; border-radius: 20px; width: 90%; max-width: 500px; max-height: 85vh; overflow-y: auto; padding: 30px; position: relative; }
        .modal-close { position: absolute; top: 15px; right: 20px; background: none; border: none; font-size: 28px; cursor: pointer; color: #aaa; transition: color 0.3s; z-index: 10; }
        .modal-close:hover { color: #3a3a3a; }
        .modal h2 { font-size: 26px; color: #3a3a3a; margin-bottom: 20px; font-family: 'Playfair Display', serif; }
        .empty-cart { text-align: center; color: #8b7a5e; padding: 30px 0; }
        .cart-notice {
            background: #fff3cd; border: 1px solid #ffc107; border-radius: 12px;
            padding: 12px 16px; margin-bottom: 15px; font-size: 13px; color: #856404;
            display: flex; align-items: center; gap: 10px;
        }
        .cart-item { display: flex; justify-content: space-between; align-items: center; padding: 12px 0; border-bottom: 1px solid #f0e6d3; }
        .cart-item-info h4 { font-size: 15px; color: #3a3a3a; }
        .cart-item-info p { font-size: 13px; color: #8b7a5e; }
        .cart-item-price { font-size: 18px; font-weight: 700; color: #6B8E23; }
        .cart-item-remove { background: none; border: none; color: #8B0000; cursor: pointer; font-size: 18px; margin-left: 10px; }
        .cart-total { display: flex; justify-content: space-between; align-items: center; padding: 20px 0; font-size: 20px; font-weight: 700; color: #3a3a3a; }
        .cart-total .total-price { color: #C75B39; font-size: 24px; font-family: 'Playfair Display', serif; }
        .pay-btn { width: 100%; background: #C75B39; color: white; border: none; padding: 16px; border-radius: 30px; font-size: 18px; font-weight: 700; cursor: pointer; transition: all 0.3s; margin-top: 10px; }
        .pay-btn:hover { background: #a84828; transform: scale(1.02); }
        .success-btn { background: #6B8E23; }
        .success-btn:hover { background: #556b1a; }
        .payment-form { display: flex; flex-direction: column; gap: 15px; }
        .payment-form label { font-size: 13px; font-weight: 600; color: #6b5a3e; margin-bottom: -10px; }
        .payment-form input { padding: 14px 18px; border: 2px solid #f0e6d3; border-radius: 12px; font-size: 16px; outline: none; transition: border-color 0.3s; }
        .payment-form input:focus { border-color: #C75B39; }
        .card-row { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        .payment-methods { display: flex; gap: 10px; margin-bottom: 10px; }
        .pay-method { flex: 1; padding: 12px; border: 2px solid #f0e6d3; border-radius: 12px; text-align: center; cursor: pointer; font-size: 14px; font-weight: 600; color: #6b5a3e; transition: all 0.3s; background: white; }
        .pay-method:hover, .pay-method.active { border-color: #C75B39; background: #f5ebe0; color: #C75B39; }
        .payment-summary { background: #f5ebe0; border-radius: 12px; padding: 15px; margin-top: 5px; }
        .summary-row { display: flex; justify-content: space-between; margin-bottom: 8px; }
        .summary-row span:first-child { color: #6b5a3e; }
        .summary-value { font-weight: 700; color: #3a3a3a; }
        .summary-value.green { color: #6B8E23; }
        .total-row { border-top: 1px solid #f0e6d3; padding-top: 8px; margin-bottom: 0; }
        .total-value { font-weight: 900; color: #C75B39; font-size: 20px; font-family: 'Playfair Display', serif; }
        .ssl-note { text-align: center; font-size: 12px; color: #aaa; margin-top: 10px; }
        .success-message { text-align: center; padding: 30px; }
        .check-icon { font-size: 60px; margin-bottom: 15px; }
        .success-message h3 { font-size: 24px; color: #6B8E23; margin-bottom: 10px; font-family: 'Playfair Display', serif; }
        .success-message p { color: #6b5a3e; font-size: 15px; }
        .qr-code { width: 150px; height: 150px; background: #faf8f5; border: 2px solid #f0e6d3; border-radius: 12px; margin: 20px auto; display: flex; align-items: center; justify-content: center; font-size: 80px; }
        .qr-note, .order-note { font-size: 13px; color: #8b7a5e; }
        .order-note { margin-top: 5px; }

        /* PLACE DETAIL */
        .place-detail { background: white; border-radius: 20px; width: 90%; max-width: 600px; max-height: 85vh; overflow-y: auto; padding: 0; position: relative; }
        .place-detail-image { height: 200px; background-size: cover; background-position: center; position: relative; }
        .place-detail-image::after { content: ''; position: absolute; bottom: 0; left: 0; right: 0; height: 80px; background: linear-gradient(to top, rgba(0,0,0,0.5), transparent); }
        .place-detail-content { padding: 30px; }
        .place-detail-header { margin-bottom: 20px; }
        .place-detail-header h2 { font-size: 28px; color: #3a3a3a; margin-bottom: 10px; }
        .place-detail-info { display: flex; flex-direction: column; gap: 10px; margin-bottom: 25px; }
        .place-detail-products { border-top: 2px solid #f0e6d3; padding-top: 20px; }
        .place-detail-products h3 { font-size: 20px; color: #3a3a3a; margin-bottom: 15px; }
        .place-detail-product { display: flex; justify-content: space-between; align-items: flex-start; padding: 14px 0; border-bottom: 1px solid #faf8f5; gap: 12px; }
        .place-detail-product:last-child { border-bottom: none; }
        .place-detail-product-info { flex: 1; }
        .place-detail-product-info h4 { font-size: 16px; color: #3a3a3a; margin-bottom: 5px; }
        .pd-ingredients { font-size: 12px; color: #8b7a5e; font-style: italic; margin-top: 5px; line-height: 1.4; display: flex; align-items: flex-start; gap: 5px; }
        .pd-ingredients .ing-icon { flex-shrink: 0; }
        .place-detail-product-info .pd-expiry { font-size: 12px; color: #8B0000; font-weight: 600; margin-top: 4px; }
        .place-detail-product-prices { text-align: right; flex-shrink: 0; }
        .place-detail-product-prices .old-price { font-size: 14px; }
        .place-detail-product-prices .new-price { font-size: 20px; }
        .place-detail-product-prices .discount-badge { font-size: 12px; padding: 3px 10px; }
        .place-detail-close-btn { background: #C75B39; color: white; border: none; padding: 14px 30px; border-radius: 25px; cursor: pointer; font-size: 16px; font-weight: 600; margin-top: 20px; width: 100%; transition: all 0.3s; }
        .place-detail-close-btn:hover { background: #a84828; }

        /* FOOTER */
        footer { background: #3a3a3a; color: #ccc; padding: 40px 20px; margin-top: 50px; }
        .footer-inner { max-width: 1200px; margin: 0 auto; display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 30px; }
        .footer-col h4 { color: #C75B39; margin-bottom: 15px; font-size: 18px; font-family: 'Playfair Display', serif; }
        .footer-col p, .footer-col a { color: #aaa; font-size: 14px; text-decoration: none; display: block; margin-bottom: 8px; transition: color 0.3s; }
        .footer-col a:hover { color: #C75B39; }
        .footer-bottom { max-width: 1200px; margin: 30px auto 0; padding-top: 20px; border-top: 1px solid #555; text-align: center; font-size: 13px; color: #888; }

        /* RESPONSIVE */
        @media (max-width: 768px) {
            .header-inner { flex-direction: column; }
            .hero h1 { font-size: 32px; }
            .cards-grid { grid-template-columns: 1fr; }
            .filter-bar { flex-direction: column; align-items: flex-start; }
            .search-box { width: 100%; margin-left: 0; }
            .chat-messages { height: 300px; }
            .product-item { flex-direction: column; }
            .product-prices { text-align: left; display: flex; align-items: center; gap: 10px; flex-wrap: wrap; }
            .place-detail-product { flex-direction: column; }
            .place-detail-product-prices { text-align: left; display: flex; align-items: center; gap: 10px; flex-wrap: wrap; }
            .reviews-summary { flex-direction: column; align-items: flex-start; }
            .reviews-grid { grid-template-columns: 1fr; }
        }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .update-notice { background: #fff3cd; border: 1px solid #ffc107; border-radius: 12px; padding: 15px 20px; margin-bottom: 25px; display: flex; align-items: center; gap: 10px; font-size: 14px; color: #856404; }
        .update-notice .pulse { width: 10px; height: 10px; background: #6B8E23; border-radius: 50%; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { box-shadow: 0 0 0 0 rgba(107,142,35,0.4); } 70% { box-shadow: 0 0 0 10px rgba(107,142,35,0); } 100% { box-shadow: 0 0 0 0 rgba(107,142,35,0); } }
        .time-badge { background: #8B0000; color: white; padding: 4px 12px; border-radius: 15px; font-size: 12px; font-weight: 600; display: inline-block; margin-top: 10px; }
    </style>
</head>
<body>

<header>
    <div class="header-inner">
        <a href="#" class="logo">
            <div class="logo-icon">🥗</div>
            <div>
                SmartFood
                <span>Еда для тех, кто ищет выгоду</span>
            </div>
        </a>
        <nav>
            <button class="active" data-tab="catalog">🏪 Каталог</button>
            <button data-tab="map">🗺️ Карта</button>
            <button data-tab="how">❓ Как это работает</button>
            <button data-tab="safety">🛡️ Безопасность</button>
            <button data-tab="support">💬 Поддержка</button>
            <button data-tab="reviews">⭐ Отзывы</button>
        </nav>
        <div class="header-actions">
            <div class="date-display" id="currentDate"></div>
            <button class="cart-btn" id="openCartBtn">
                🛒 Корзина
                <span class="cart-count" id="cartCount">0</span>
            </button>
        </div>
    </div>
</header>

<section class="hero">
    <div class="hero-content">
        <h1>Свежая еда со скидкой <em>до 80%</em></h1>
        <p>Еда для тех, кто ищет выгоду</p>
        <div class="hero-stats">
            <div class="stat"><div class="stat-num" id="statPlaces">11</div><div class="stat-label">заведений рядом</div></div>
            <div class="stat"><div class="stat-num" id="statProducts">33</div><div class="stat-label">товаров со скидкой</div></div>
            <div class="stat"><div class="stat-num">до 80%</div><div class="stat-label">экономия</div></div>
        </div>
    </div>
</section>

<!-- TAB: КАТАЛОГ -->
<div class="tab-content active" id="tab-catalog">
    <div class="update-notice">
        <div class="pulse"></div>
        <span>Ассортимент обновлён сегодня, <strong id="updateDate"></strong>. Товары выставляются с 18:00 до закрытия заведения.</span>
    </div>
    <h2 class="section-title">Заведения рядом с вами</h2>
    <p class="section-subtitle">Нажмите «В корзину», чтобы добавить товар. Скидки действуют до закрытия заведения.</p>
    <div class="filter-bar">
        <label>Фильтр:</label>
        <button class="filter-btn active" data-filter="all">Все</button>
        <button class="filter-btn" data-filter="bakery">🥐 Пекарни</button>
        <button class="filter-btn" data-filter="cafe">☕ Кофейни</button>
        <input type="text" class="search-box" id="searchBox" placeholder="🔍 Поиск по названию или продукту...">
    </div>
    <div class="cards-grid" id="cardsGrid"></div>
</div>

<!-- TAB: КАРТА -->
<div class="tab-content" id="tab-map">
    <h2 class="section-title">Карта заведений</h2>
    <p class="section-subtitle">Нажмите на метку на карте, чтобы увидеть подробную информацию о заведении и его скидках</p>
    <div class="map-container">
        <div class="map-placeholder">
            <div class="map-icon">🗺️</div>
            <p class="map-title">Интерактивная карта Москвы</p>
            <p class="map-subtitle">Кликните на цифру, чтобы открыть заведение</p>
            <div class="map-pin" style="top:25%; left:20%;" data-place="1"><span>1</span></div>
            <div class="map-pin" style="top:40%; left:35%;" data-place="2"><span>2</span></div>
            <div class="map-pin" style="top:30%; left:50%;" data-place="3"><span>3</span></div>
            <div class="map-pin" style="top:50%; left:25%;" data-place="4"><span>4</span></div>
            <div class="map-pin" style="top:45%; left:60%;" data-place="5"><span>5</span></div>
            <div class="map-pin" style="top:60%; left:45%;" data-place="6"><span>6</span></div>
            <div class="map-pin" style="top:55%; left:70%;" data-place="7"><span>7</span></div>
            <div class="map-pin" style="top:35%; left:75%;" data-place="8"><span>8</span></div>
            <div class="map-pin" style="top:70%; left:30%;" data-place="9"><span>9</span></div>
            <div class="map-pin" style="top:65%; left:55%;" data-place="10"><span>10</span></div>
            <div class="map-pin" style="top:75%; left:70%;" data-place="11"><span>11</span></div>
        </div>
        <div class="map-legend">
            <div class="legend-item"><div class="legend-dot" style="background:#C75B39;"></div> Пекарни</div>
            <div class="legend-item"><div class="legend-dot" style="background:#8B4513;"></div> Кофейни</div>
            <div class="legend-item"><div class="legend-dot" style="background:#8B0000;"></div> Срочная скидка (75-80%)</div>
        </div>
    </div>
</div>

<!-- TAB: КАК ЭТО РАБОТАЕТ -->
<div class="tab-content" id="tab-how">
    <h2 class="section-title">Как это работает</h2>
    <p class="section-subtitle">Всего 4 простых шага до вкусной еды со скидкой</p>
    <div class="steps">
        <div class="step">
            <div class="step-num">1</div>
            <h3>Откройте сайт</h3>
            <p>Зайдите на SmartFood после 18:00 и посмотрите список заведений рядом с вами. Ассортимент обновляется каждый день.</p>
        </div>
        <div class="step">
            <div class="step-num">2</div>
            <h3>Выберите продукты</h3>
            <p>Посмотрите скидки 50%, 60%, 70%, 75% или 80% на продукты с истекающим сроком годности. Все товары свежие — просто их нужно продать сегодня на ужин.</p>
        </div>
        <div class="step">
            <div class="step-num">3</div>
            <h3>Оплатите онлайн</h3>
            <p>Добавьте товары в корзину и оплатите удобным способом. Получите QR-код для получения заказа.</p>
        </div>
        <div class="step">
            <div class="step-num">4</div>
            <h3>Заберите заказ</h3>
            <p>Придите в заведение до его закрытия, покажите QR-код и заберите свои продукты со скидкой до 80%! <strong>Все заказы выдаются только самовывозом.</strong></p>
        </div>
    </div>
    <div class="benefits-block">
        <h3 class="benefits-title">💡 Почему это выгодно?</h3>
        <div class="benefits-grid">
            <div><h4 class="benefit-title">Для покупателей</h4><p class="benefit-text">Экономия от 50% до 80% на качественных продуктах от проверенных заведений Москвы.</p></div>
            <div><h4 class="benefit-title">Для заведений</h4><p class="benefit-text">Сокращение пищевых отходов и дополнительный доход вместо списания продукции.</p></div>
            <div><h4 class="benefit-title">Для экологии</h4><p class="benefit-text">Меньше еды выбрасывается — меньше вреда для окружающей среды.</p></div>
        </div>
    </div>
</div>

<!-- TAB: БЕЗОПАСНОСТЬ -->
<div class="tab-content" id="tab-safety">
    <h2 class="section-title">Безопасность и качество</h2>
    <p class="section-subtitle">Мы серьёзно относимся к качеству продуктов. Вот как мы гарантируем безопасность.</p>
    <div class="safety-grid">
        <div class="safety-card"><div class="s-icon">🔍</div><h3>Контроль срока годности</h3><p>Все продукты продаются строго в рамках срока годности. Мы сотрудничаем только с заведениями, которые соблюдают санитарные нормы. Продукт снимается с продажи за 2 часа до истечения срока.</p><div class="rating-stars">★★★★★</div></div>
        <div class="safety-card"><div class="s-icon">✅</div><h3>Проверенные партнёры</h3><p>Каждое заведение проходит проверку перед подключением к платформе. Мы работаем только с лицензированными пекарнями и кофейнями Москвы, имеющими все необходимые сертификаты.</p><div class="rating-stars">★★★★★</div></div>
        <div class="safety-card"><div class="s-icon">🌡️</div><h3>Правильное хранение</h3><p>Продукты хранятся при правильной температуре до момента продажи. Мы контролируем условия хранения через партнёрские соглашения с заведениями.</p><div class="rating-stars">★★★★☆</div></div>
        <div class="safety-card"><div class="s-icon">⭐</div><h3>Система рейтингов</h3><p>Покупатели оставляют отзывы и оценки после каждой покупки. Заведения с низким рейтингом автоматически отключаются от платформы. Прозрачность — наш приоритет.</p><div class="rating-stars">★★★★★</div></div>
        <div class="safety-card"><div class="s-icon">📋</div><h3>Полная информация</h3><p>На каждом товаре указан точный срок годности, состав и условия хранения. Вы всегда знаете, что покупаете. Никаких скрытых условий.</p><div class="rating-stars">★★★★★</div></div>
        <div class="safety-card"><div class="s-icon">💬</div><h3>Поддержка 24/7</h3><p>Если у вас возникли вопросы или проблемы с качеством — наша служба поддержки решит их в течение часа. Полный возврат средств при любом несоответствии.</p><div class="rating-stars">★★★★★</div></div>
    </div>
</div>

<!-- TAB: ПОДДЕРЖКА -->
<div class="tab-content" id="tab-support">
    <h2 class="section-title">Чат-бот поддержки</h2>
    <p class="section-subtitle">Задайте вопрос или выберите тему из быстрых ответов</p>
    <div class="chat-container">
        <div class="chat-header">
            <div class="chat-header-icon">🤖</div>
            <div class="chat-header-info">
                <h3>SmartFood Бот</h3>
                <p><span class="chat-status"></span>Онлайн • Отвечает мгновенно</p>
            </div>
        </div>
        <div class="chat-messages" id="chatMessages">
            <div class="chat-message bot">Здравствуйте! 👋 Я бот-помощник SmartFood. Чем могу помочь?</div>
        </div>
        <div class="chat-quick-replies">
            <button class="quick-reply" data-q="Как сделать заказ?">Как сделать заказ?</button>
            <button class="quick-reply" data-q="Какие скидки есть?">Какие скидки есть?</button>
            <button class="quick-reply" data-q="Как получить заказ?">Как получить заказ?</button>
            <button class="quick-reply" data-q="Безопасно ли это?">Безопасно ли это?</button>
            <button class="quick-reply" data-q="Время работы">Время работы</button>
            <button class="quick-reply" data-q="Связаться с оператором">Связаться с оператором</button>
        </div>
        <div class="chat-input-area">
            <input type="text" class="chat-input" id="chatInput" placeholder="Напишите ваш вопрос...">
            <button class="chat-send" id="chatSendBtn">Отправить</button>
        </div>
    </div>
</div>

<!-- TAB: ОТЗЫВЫ -->
<div class="tab-content" id="tab-reviews">
    <h2 class="section-title">Отзывы наших покупателей</h2>
    <p class="section-subtitle">Что говорят о SmartFood те, кто уже попробовал</p>
    <div class="reviews-summary">
        <div class="reviews-avg">
            <div class="reviews-avg-num">4.8</div>
            <div class="reviews-avg-stars">★★★★★</div>
            <div class="reviews-avg-count">на основе 247 отзывов</div>
        </div>
        <div class="reviews-bars">
            <div class="review-bar-row"><span>5 ★</span><div class="review-bar"><div class="review-bar-fill" style="width:78%"></div></div><span>78%</span></div>
            <div class="review-bar-row"><span>4 ★</span><div class="review-bar"><div class="review-bar-fill" style="width:15%"></div></div><span>15%</span></div>
            <div class="review-bar-row"><span>3 ★</span><div class="review-bar"><div class="review-bar-fill" style="width:5%"></div></div><span>5%</span></div>
            <div class="review-bar-row"><span>2 ★</span><div class="review-bar"><div class="review-bar-fill" style="width:1%"></div></div><span>1%</span></div>
            <div class="review-bar-row"><span>1 ★</span><div class="review-bar"><div class="review-bar-fill" style="width:1%"></div></div><span>1%</span></div>
        </div>
    </div>
    <div class="reviews-grid" id="reviewsGrid"></div>
</div>

<!-- МОДАЛКА: КОРЗИНА -->
<div class="modal-overlay" id="cartModal">
    <div class="modal">
        <button class="modal-close" id="closeCartBtn">×</button>
        <h2>🛒 Ваша корзина</h2>
        <div id="cartItems">
            <p class="empty-cart">Корзина пуста. Добавьте товары из каталога!</p>
        </div>
        <div class="cart-total" id="cartTotal" style="display:none;">
            <span>Итого:</span>
            <span class="total-price" id="totalPrice">0 ₽</span>
        </div>
        <button class="pay-btn" id="payBtn" style="display:none;">Перейти к оплате</button>
    </div>
</div>

<!-- МОДАЛКА: ОПЛАТА -->
<div class="modal-overlay" id="paymentModal">
    <div class="modal">
        <button class="modal-close" id="closePaymentBtn">×</button>
        <div id="paymentForm">
            <h2>💳 Оплата заказа</h2>
            <div class="payment-methods">
                <div class="pay-method active" data-method="card">💳 Карта</div>
                <div class="pay-method" data-method="sbp">📱 СБП</div>
            </div>
            <div class="payment-form">
                <label>Номер карты</label>
                <input type="text" id="cardNumber" placeholder="0000 0000 0000 0000" maxlength="19">
                <label>Имя владельца</label>
                <input type="text" id="cardName" placeholder="IVAN IVANOV">
                <div class="card-row">
                    <div><label>Срок</label><input type="text" id="cardExpiry" placeholder="MM/ГГ" maxlength="5"></div>
                    <div><label>CVV</label><input type="password" id="cardCvv" placeholder="•••" maxlength="3"></div>
                </div>
                <label>Email для чека</label>
                <input type="email" id="cardEmail" placeholder="your@email.com">
                <div class="payment-summary">
                    <div class="summary-row"><span>Сумма заказа:</span><span class="summary-value" id="payAmount">0 ₽</span></div>
                    <div class="summary-row"><span>Комиссия:</span><span class="summary-value green">0 ₽</span></div>
                    <div class="summary-row total-row"><span>К оплате:</span><span class="summary-value total-value" id="payTotal">0 ₽</span></div>
                </div>
                <button class="pay-btn" id="processPaymentBtn">Оплатить</button>
                <p class="ssl-note">🔒 Платёж защищён SSL-шифрованием</p>
            </div>
        </div>
        <div id="paymentSuccess" style="display:none;">
            <div class="success-message">
                <div class="check-icon">✅</div>
                <h3>Оплата прошла успешно!</h3>
                <p>Ваш заказ оплачен. Покажите QR-код в заведении для получения продуктов.</p>
                <div class="qr-code">📱</div>
                <p class="qr-note">QR-код отправлен на вашу почту</p>
                <p class="order-note">Номер заказа: <strong id="orderNumber"></strong></p>
                <button class="pay-btn success-btn" id="closeSuccessBtn">Отлично!</button>
            </div>
        </div>
    </div>
</div>

<!-- МОДАЛКА: ДЕТАЛИ ЗАВЕДЕНИЯ -->
<div class="modal-overlay" id="placeDetailModal">
    <div class="place-detail">
        <button class="modal-close" id="closePlaceDetailBtn" style="z-index:10; background:white; width:36px; height:36px; border-radius:50%; display:flex; align-items:center; justify-content:center;">×</button>
        <div class="place-detail-image" id="placeDetailImage"></div>
        <div class="place-detail-content">
            <div class="place-detail-header">
                <h2 id="placeDetailName"></h2>
                <span class="card-type" id="placeDetailType"></span>
            </div>
            <div class="place-detail-info">
                <div class="card-info-row"><span class="icon">📍</span> <span id="placeDetailAddress"></span></div>
                <div class="card-info-row"><span class="icon">🚇</span> м. <span id="placeDetailMetro"></span></div>
                <div class="card-info-row"><span class="icon">🕐</span> <span id="placeDetailHours"></span></div>
                <div class="card-info-row"><span class="icon">⭐</span> Рейтинг: <span id="placeDetailRating"></span>/5.0</div>
                <div class="time-badge">🕕 С 18:00 до закрытия</div>
            </div>
            <div class="place-detail-products">
                <h3>🏷️ Скидки сегодня</h3>
                <div id="placeDetailProducts"></div>
            </div>
            <button class="place-detail-close-btn" id="placeDetailCloseBtn">Закрыть</button>
        </div>
    </div>
</div>

<footer>
    <div class="footer-inner">
        <div class="footer-col">
            <h4>🥗 SmartFood</h4>
            <p>Платформа фудшеринга в Москве. Спасаем еду от утилизации, помогаем экономить.</p>
        </div>
        <div class="footer-col">
            <h4>Навигация</h4>
            <a href="#" data-nav="catalog">Каталог</a>
            <a href="#" data-nav="map">Карта</a>
            <a href="#" data-nav="how">Как это работает</a>
            <a href="#" data-nav="safety">Безопасность</a>
            <a href="#" data-nav="support">Поддержка</a>
            <a href="#" data-nav="reviews">Отзывы</a>
        </div>
        <div class="footer-col">
            <h4>Партнёрам</h4>
            <a href="#">Подключить заведение</a>
            <a href="#">Условия сотрудничества</a>
            <a href="#">Для бизнеса</a>
        </div>
        <div class="footer-col">
            <h4>Контакты</h4>
            <p>📧 hello@smartfood.ru</p>
            <p>📞 8 (800) 555-35-35</p>
            <p>📍 Москва, Россия</p>
        </div>
    </div>
    <div class="footer-bottom">© 2026 SmartFood. Все права защищены. Сделано с ❤️ для Москвы.</div>
</footer>

<script>
    // ДАННЫЕ ЗАВЕДЕНИЙ (с телефонами)
    const placesData = [
        { id: 1, name: "Хлеб Насущный", type: "bakery", typeLabel: "Пекарня", address: "ул. Тверская, 15", metro: "Тверская", hours: "08:00 – 22:00", phone: "+7 (495) 123-45-67", distance: "0.3 км", rating: 4.8, image: "https://images.unsplash.com/photo-1509440159596-0249088772ff?w=400&auto=format&fit=crop", products: [
            { name: "Круассан с миндалём", oldPrice: 290, newPrice: 145, discount: 50, expiry: "до 22:00 сегодня", ingredients: "Мука пшеничная, масло сливочное, миндальная паста, сахар, дрожжи, яйца, соль, ванилин" },
            { name: "Багет французский", oldPrice: 180, newPrice: 54, discount: 70, expiry: "до 22:00 сегодня", ingredients: "Мука пшеничная в/с, вода, дрожжи, соль, сахар" },
            { name: "Эклер ванильный", oldPrice: 220, newPrice: 88, discount: 60, expiry: "до 21:00 сегодня", ingredients: "Заварное тесто, крем заварной ванильный, сахарная пудра, ванильный экстракт, яйца, масло сливочное" }
        ]},
        { id: 2, name: "Буше", type: "bakery", typeLabel: "Пекарня-кондитерская", address: "ул. Арбат, 24", metro: "Арбатская", hours: "08:00 – 23:00", phone: "+7 (495) 234-56-78", distance: "0.5 км", rating: 4.9, image: "https://images.unsplash.com/photo-1555507036-ab1f4038808a?w=400&auto=format&fit=crop", products: [
            { name: "Торт «Наполеон» (кусочек)", oldPrice: 380, newPrice: 95, discount: 75, expiry: "до 23:00 сегодня", ingredients: "Слоёное тесто, крем заварной, масло сливочное, сахар, яйца, мука, ванилин" },
            { name: "Улитка с изюмом", oldPrice: 195, newPrice: 98, discount: 50, expiry: "до 22:00 сегодня", ingredients: "Слоёное тесто, изюм, корица, сахар, масло сливочное, яйца" },
            { name: "Киш лорен", oldPrice: 320, newPrice: 128, discount: 60, expiry: "до 21:00 сегодня", ingredients: "Песочное тесто, бекон, сыр эмменталь, яйца, сливки, мускатный орех, соль, перец" }
        ]},
        { id: 3, name: "Волконский", type: "bakery", typeLabel: "Пекарня", address: "ул. Покровка, 7", metro: "Китай-город", hours: "07:30 – 22:00", phone: "+7 (495) 345-67-89", distance: "0.8 км", rating: 4.7, image: "https://images.unsplash.com/photo-1585476263060-b7a6b710f2a1?w=400&auto=format&fit=crop", products: [
            { name: "Хлеб «Бородинский»", oldPrice: 160, newPrice: 32, discount: 80, expiry: "до 22:00 сегодня", ingredients: "Мука ржаная обдирная, мука пшеничная, солод ржаной, кориандр, тмин, соль, закваска" },
            { name: "Чиабатта с оливками", oldPrice: 210, newPrice: 63, discount: 70, expiry: "до 21:00 сегодня", ingredients: "Мука пшеничная, вода, оливковое масло, оливки чёрные, дрожжи, соль, розмарин" },
            { name: "Пирожок с вишней", oldPrice: 145, newPrice: 73, discount: 50, expiry: "до 20:00 сегодня", ingredients: "Дрожжевое тесто, вишня, сахар, крахмал, корица, ванилин" }
        ]},
        { id: 4, name: "Cinnabon", type: "cafe", typeLabel: "Кофейня-пекарня", address: "ТЦ «Европейский», пл. Киевского Вокзала, 2", metro: "Киевская", hours: "10:00 – 22:00", phone: "+7 (495) 456-78-90", distance: "1.2 км", rating: 4.6, image: "https://images.unsplash.com/photo-1555507036-ab1f4038808a?w=400&auto=format&fit=crop", products: [
            { name: "Классический синнабон", oldPrice: 310, newPrice: 124, discount: 60, expiry: "до 22:00 сегодня", ingredients: "Дрожжевое тесто, корица, сахар, масло сливочное, крем-чиз, ванильный экстракт" },
            { name: "Пепперони ролл", oldPrice: 280, newPrice: 70, discount: 75, expiry: "до 21:00 сегодня", ingredients: "Дрожжевое тесто, пепперони, сыр моцарелла, томатный соус, орегано, чеснок" },
            { name: "Мини-синнабон (3 шт)", oldPrice: 250, newPrice: 125, discount: 50, expiry: "до 22:00 сегодня", ingredients: "Дрожжевое тесто, корица, сахар, масло сливочное, крем-чиз, ваниль" }
        ]},
        { id: 5, name: "Кофемания", type: "cafe", typeLabel: "Кофейня-ресторан", address: "ул. Большая Никитская, 14", metro: "Охотный Ряд", hours: "08:00 – 00:00", phone: "+7 (495) 567-89-01", distance: "0.4 км", rating: 4.8, image: "https://images.unsplash.com/photo-1501339847302-ac426a4a7cbb?w=400&auto=format&fit=crop", products: [
            { name: "Чизкейк Нью-Йорк", oldPrice: 420, newPrice: 126, discount: 70, expiry: "до 00:00 сегодня", ingredients: "Сыр сливочный, печенье песочное, масло сливочное, сахар, яйца, ваниль, лимонный сок" },
            { name: "Сэндвич с лососем", oldPrice: 490, newPrice: 196, discount: 60, expiry: "до 22:00 сегодня", ingredients: "Хлеб чиабатта, лосось слабосолёный, сыр сливочный, огурец свежий, укроп, лимон" },
            { name: "Маффин шоколадный", oldPrice: 230, newPrice: 46, discount: 80, expiry: "до 23:00 сегодня", ingredients: "Мука пшеничная, какао-порошок, шоколад тёмный, сахар, яйца, масло сливочное, разрыхлитель" }
        ]},
        { id: 6, name: "Surf Coffee", type: "cafe", typeLabel: "Кофейня", address: "ул. Мясницкая, 24", metro: "Тургеневская", hours: "08:00 – 22:00", phone: "+7 (495) 678-90-12", distance: "0.6 км", rating: 4.7, image: "https://images.unsplash.com/photo-1554118811-1e0d58224f24?w=400&auto=format&fit=crop", products: [
            { name: "Авокадо-тост", oldPrice: 390, newPrice: 156, discount: 60, expiry: "до 20:00 сегодня", ingredients: "Хлеб цельнозерновой, авокадо, яйцо пашот, томаты черри, соль морская, перец, лимонный сок" },
            { name: "Круассан с ветчиной", oldPrice: 310, newPrice: 93, discount: 70, expiry: "до 21:00 сегодня", ingredients: "Круассан, ветчина, сыр эмменталь, яйца, сливки, мускатный орех" },
            { name: "Банановый хлеб", oldPrice: 220, newPrice: 110, discount: 50, expiry: "до 22:00 сегодня", ingredients: "Бананы спелые, мука пшеничная, сахар, яйца, масло сливочное, разрыхлитель, ваниль, грецкие орехи" }
        ]},
        { id: 7, name: "Формула Хлеба", type: "bakery", typeLabel: "Пекарня", address: "ул. Сретенка, 19", metro: "Тургеневская", hours: "07:00 – 21:00", phone: "+7 (495) 789-01-23", distance: "0.9 км", rating: 4.5, image: "https://images.unsplash.com/photo-1549931319-a545dcf3bc73?w=400&auto=format&fit=crop", products: [
            { name: "Хлеб «Дарницкий»", oldPrice: 95, newPrice: 19, discount: 80, expiry: "до 21:00 сегодня", ingredients: "Мука ржаная обойная, мука пшеничная 1 сорт, вода, закваска, соль" },
            { name: "Булочка с маком", oldPrice: 120, newPrice: 48, discount: 60, expiry: "до 20:00 сегодня", ingredients: "Дрожжевое тесто, мак, сахар, ванилин, яйца, молоко" },
            { name: "Пирог с яблоком (кусочек)", oldPrice: 180, newPrice: 45, discount: 75, expiry: "до 21:00 сегодня", ingredients: "Песочное тесто, яблоки, сахар, корица, крахмал, лимонный сок, масло сливочное" }
        ]},
        { id: 8, name: "One Price Coffee", type: "cafe", typeLabel: "Кофейня", address: "ул. Рождественка, 12", metro: "Лубянка", hours: "08:00 – 21:00", phone: "+7 (495) 890-12-34", distance: "0.7 км", rating: 4.6, image: "https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?w=400&auto=format&fit=crop", products: [
            { name: "Сэндвич с курицей", oldPrice: 340, newPrice: 102, discount: 70, expiry: "до 20:00 сегодня", ingredients: "Чиабатта, куриное филе гриль, сыр моцарелла, томаты, руккола, соус песто" },
            { name: "Кекс лимонный", oldPrice: 190, newPrice: 95, discount: 50, expiry: "до 21:00 сегодня", ingredients: "Мука пшеничная, сахар, яйца, масло сливочное, лимон, разрыхлитель, ваниль, сахарная пудра" },
            { name: "Хлебцы с паштетом", oldPrice: 260, newPrice: 104, discount: 60, expiry: "до 19:00 сегодня", ingredients: "Хлебцы цельнозерновые, паштет из куриной печени, масло сливочное, лук карамелизированный, тимьян" }
        ]},
        { id: 9, name: "Шоколадница", type: "cafe", typeLabel: "Кофейня", address: "ул. Кузнецкий Мост, 7", metro: "Лубянка", hours: "08:00 – 23:00", phone: "+7 (495) 901-23-45", distance: "0.5 км", rating: 4.4, image: "https://images.unsplash.com/photo-1511920170033-f8396924c348?w=400&auto=format&fit=crop", products: [
            { name: "Тирамису", oldPrice: 350, newPrice: 88, discount: 75, expiry: "до 23:00 сегодня", ingredients: "Сыр маскарпоне, печенье савоярди, кофе эспрессо, яйца, сахар, какао-порошок, амаретто" },
            { name: "Круассан с шоколадом", oldPrice: 210, newPrice: 84, discount: 60, expiry: "до 22:00 сегодня", ingredients: "Слоёное тесто, шоколад тёмный, масло сливочное, сахарная пудра, какао" },
            { name: "Салат Цезарь", oldPrice: 420, newPrice: 210, discount: 50, expiry: "до 21:00 сегодня", ingredients: "Салат романо, куриное филе, сыр пармезан, сухарики, соус цезарь, томаты черри" }
        ]},
        { id: 10, name: "Даблби", type: "cafe", typeLabel: "Кофейня", address: "ул. Большая Дмитровка, 9", metro: "Театральная", hours: "08:00 – 22:00", phone: "+7 (495) 012-34-56", distance: "0.4 км", rating: 4.7, image: "https://images.unsplash.com/photo-1445116572660-236099ec97a0?w=400&auto=format&fit=crop", products: [
            { name: "Сырники со сметаной", oldPrice: 320, newPrice: 96, discount: 70, expiry: "до 20:00 сегодня", ingredients: "Творог 9%, яйца, мука, сахар, ваниль, сметана 20%, соль" },
            { name: "Тост с авокадо", oldPrice: 370, newPrice: 148, discount: 60, expiry: "до 19:00 сегодня", ingredients: "Хлеб тостовый, авокадо, яйцо пашот, семена чиа, соль, перец, оливковое масло" },
            { name: "Брауни", oldPrice: 240, newPrice: 48, discount: 80, expiry: "до 22:00 сегодня", ingredients: "Шоколад тёмный 70%, масло сливочное, сахар, яйца, мука, какао, грецкие орехи, ваниль" }
        ]},
        { id: 11, name: "Пекарня «Люди любят»", type: "bakery", typeLabel: "Пекарня", address: "ул. Пятницкая, 29", metro: "Новокузнецкая", hours: "08:00 – 21:00", phone: "+7 (495) 111-22-33", distance: "1.1 км", rating: 4.8, image: "https://images.unsplash.com/photo-1555507036-ab1f4038808a?w=400&auto=format&fit=crop", products: [
            { name: "Хлеб на закваске", oldPrice: 250, newPrice: 63, discount: 75, expiry: "до 21:00 сегодня", ingredients: "Мука пшеничная цельнозерновая, вода, закваска натуральная, соль морская" },
            { name: "Фокачча с розмарином", oldPrice: 290, newPrice: 116, discount: 60, expiry: "до 20:00 сегодня", ingredients: "Мука пшеничная, оливковое масло, розмарин свежий, чеснок, соль морская, дрожжи" },
            { name: "Печенье овсяное (уп.)", oldPrice: 180, newPrice: 90, discount: 50, expiry: "до 21:00 сегодня", ingredients: "Овсяные хлопья, мука пшеничная, сахар, масло сливочное, яйца, изюм, корица, разрыхлитель" }
        ]}
    ];

    // ДАННЫЕ ОТЗЫВОВ
    const reviewsData = [
        { name: "Анна Соколова", role: "Студентка МГУ", avatar: "А", stars: 5, text: "Нашла здесь круассаны за 145₽ вместо 290₽! Качество отличное, всё свежее. Теперь захожу каждый вечер после пар — экономлю около 500₽ в неделю. Спасибо SmartFood!", date: "21 октября 2026", place: "Хлеб Насущный" },
        { name: "Дмитрий Орлов", role: "Офисный работник", avatar: "Д", stars: 5, text: "Идеально для ужина! Беру сэндвичи и салаты в Кофемании со скидкой 60-70% после работы. Удобно, что можно оплатить онлайн и просто забрать по QR-коду. Никаких очередей!", date: "19 октября 2026", place: "Кофемания" },
        { name: "Мария Белова", role: "Мама двоих детей", avatar: "М", stars: 5, text: "Покупаю здесь выпечку для детей — всё свежее, состав натуральный. Особенно радует, что есть подробный состав каждого продукта. Брауни в Даблби за 48₽ — это находка!", date: "17 октября 2026", place: "Даблби" },
        { name: "Алексей Петров", role: "Фрилансер", avatar: "А", stars: 4, text: "Хороший сервис, большой выбор. Единственный минус — нужно успеть забрать до закрытия, иначе скидка сгорает. Но это логично. В целом очень доволен, экономия реальная.", date: "15 октября 2026", place: "Surf Coffee" },
        { name: "Екатерина Новикова", role: "Дизайнер", avatar: "Е", stars: 5, text: "Обожаю концепцию! Вкусная еда по адекватным ценам + помощь экологии. Тирамису в Шоколаднице за 88₽ вместо 350₽ — это просто космос. Рекомендую всем друзьям!", date: "12 октября 2026", place: "Шоколадница" },
        { name: "Иван Кузнецов", role: "Студент ВШЭ", avatar: "И", stars: 5, text: "Как студент с ограниченным бюджетом, этот сайт — спасение. Хлеб Бородинский за 32₽, пирог с яблоком за 45₽ — питаюсь вкусно и разнообразно. Отдельное спасибо за чат-бот!", date: "10 октября 2026", place: "Волконский" },
        { name: "Ольга Смирнова", role: "Преподаватель", avatar: "О", stars: 4, text: "Пользуюсь уже месяц. Нравится, что можно посмотреть состав и срок годности. Иногда бывают моменты, когда нужный товар уже разобрали, но это редкость. Сервис отличный!", date: "8 октября 2026", place: "Буше" },
        { name: "Николай Волков", role: "Инженер", avatar: "Н", stars: 5, text: "Синнабоны в Cinnabon со скидкой 75% — это что-то невероятное! Жена в восторге. Заказываем через сайт, забираем по дороге домой вечером. Очень удобно, спасибо!", date: "5 октября 2026", place: "Cinnabon" }
    ];

    let cart = [];

    const chatResponses = {
        'Как сделать заказ?': 'Чтобы сделать заказ:\n1️⃣ Откройте вкладку "Каталог"\n2️⃣ Выберите заведение и товары со скидкой\n3️⃣ Нажмите "В корзину"\n4️⃣ Перейдите к оплате\n5️⃣ Получите QR-код и заберите заказ в заведении!\n\nВсё просто! 😊',
        'Какие скидки есть?': 'У нас скидки от 50% до 80%! 🎉\n\n• 50% — базовая скидка\n• 60% — хорошая скидка\n• 70% — отличная скидка\n• 75% — супер скидка\n• 80% — максимальная скидка!\n\nСкидки зависят от времени до закрытия заведения. Чем позже — тем выгоднее! 🕕',
        'Как получить заказ?': 'После оплаты вы получите QR-код на email 📧\n\nПридите в заведение до его закрытия, покажите QR-код сотруднику и заберите свои продукты!\n\n⚠️ Важно: товары нужно забрать до закрытия заведения, иначе скидка сгорит.',
        'Безопасно ли это?': 'Абсолютно безопасно! ✅\n\n• Все продукты продаются в рамках срока годности\n• Мы работаем только с проверенными заведениями\n• Продукты хранятся при правильной температуре\n• Есть система рейтингов и отзывов\n• Полный возврат средств при проблемах\n\nВаше здоровье — наш приоритет! 🛡️',
        'Время работы': 'Товары со скидкой выставляются каждый день с 18:00 до закрытия заведения 🕕\n\nВремя работы заведений:\n• Пекарни: обычно до 21:00-23:00\n• Кофейни: обычно до 22:00-00:00\n\nТочное время смотрите в карточке заведения в каталоге!',
        'Связаться с оператором': 'Я передам ваш запрос оператору! 👨‍💼\n\nВы также можете связаться с нами:\n📧 hello@smartfood.ru\n📞 8 (800) 555-35-35\n\nВремя работы поддержки: 9:00 - 21:00\n\nОбычно отвечаем в течение 15 минут! ⚡'
    };

    function setCurrentDate() {
        const now = new Date();
        const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
        const dateStr = now.toLocaleDateString('ru-RU', options);
        document.getElementById('currentDate').textContent = dateStr.charAt(0).toUpperCase() + dateStr.slice(1);
        document.getElementById('updateDate').textContent = dateStr;
    }

    function renderCards(data) {
        const grid = document.getElementById('cardsGrid');
        grid.innerHTML = '';
        data.forEach(place => {
            const card = document.createElement('div');
            card.className = 'place-card';
            card.dataset.type = place.type;
            card.dataset.name = place.name.toLowerCase();
            let productsHTML = '';
            place.products.forEach((prod, idx) => {
                productsHTML += `
                    <div class="product-item">
                        <div class="product-info-block">
                            <div class="product-name">${prod.name}</div>
                            <div class="product-ingredients"><span class="ing-icon">🧾</span><span class="ing-text">${prod.ingredients}</span></div>
                            <div class="product-expiry">⏰ ${prod.expiry}</div>
                        </div>
                        <div class="product-prices">
                            <div class="old-price">${prod.oldPrice} ₽</div>
                            <div class="new-price">${prod.newPrice} ₽</div>
                            <div class="discount-badge">-${prod.discount}%</div>
                            <button class="add-btn" id="btn-${place.id}-${idx}" data-place="${place.id}" data-idx="${idx}">В корзину</button>
                        </div>
                    </div>`;
            });
            card.innerHTML = `
                <div class="card-image" style="background-image: url('${place.image}');"></div>
                <div class="card-header">
                    <h3>${place.name}</h3>
                    <span class="card-type">${place.typeLabel}</span>
                    <span class="card-distance">📍 ${place.distance}</span>
                    <div class="time-badge">🕕 С 18:00 до закрытия</div>
                </div>
                <div class="card-body">
                    <div class="card-info">
                        <div class="card-info-row"><span class="icon">📍</span> ${place.address} (м. ${place.metro})</div>
                        <div class="card-info-row"><span class="icon">🕐</span> ${place.hours}</div>
                        <div class="card-info-row phone-row"><span class="icon">📞</span> <a href="tel:${place.phone.replace(/\s/g, '')}">${place.phone}</a></div>
                        <div class="card-info-row"><span class="icon">⭐</span> Рейтинг: ${place.rating}/5.0</div>
                    </div>
                    <div class="products-list"><h4>🏷️ Скидки сегодня</h4>${productsHTML}</div>
                </div>`;
            grid.appendChild(card);
        });
        document.querySelectorAll('.add-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                addToCart(parseInt(this.dataset.place), parseInt(this.dataset.idx), this);
            });
        });
    }

    function renderReviews() {
        const grid = document.getElementById('reviewsGrid');
        if (!grid) return;
        grid.innerHTML = '';
        reviewsData.forEach(review => {
            const starsHTML = '★'.repeat(review.stars) + '☆'.repeat(5 - review.stars);
            const card = document.createElement('div');
            card.className = 'review-card';
            card.innerHTML = `
                <div class="review-header">
                    <div class="review-avatar">${review.avatar}</div>
                    <div class="review-author">
                        <div class="review-author-name">${review.name}</div>
                        <div class="review-author-role">${review.role}</div>
                    </div>
                    <div class="review-stars">${starsHTML}</div>
                </div>
                <div class="review-text">"${review.text}"</div>
                <div class="review-meta">
                    <span>${review.date}</span>
                    <span class="review-place">${review.place}</span>
                </div>`;
            grid.appendChild(card);
        });
    }

    function filterCards(type, btn) {
        document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        document.querySelectorAll('.place-card').forEach(card => {
            card.style.display = (type === 'all' || card.dataset.type === type) ? 'block' : 'none';
        });
    }

    function searchCards(query) {
        const q = query.toLowerCase();
        document.querySelectorAll('.place-card').forEach(card => {
            card.style.display = (card.dataset.name.includes(q) || card.textContent.toLowerCase().includes(q)) ? 'block' : 'none';
        });
    }

    function addToCart(placeId, productIdx, btn) {
        const place = placesData.find(p => p.id === placeId);
        const product = place.products[productIdx];
        const cartItem = { id: `${placeId}-${productIdx}`, name: product.name, place: place.name, price: product.newPrice, discount: product.discount };
        const exists = cart.find(item => item.id === cartItem.id);
        if (exists) {
            cart = cart.filter(item => item.id !== cartItem.id);
            btn.textContent = 'В корзину';
            btn.classList.remove('added');
        } else {
            cart.push(cartItem);
            btn.textContent = '✓ Добавлено';
            btn.classList.add('added');
        }
        updateCartCount();
    }

    function updateCartCount() {
        document.getElementById('cartCount').textContent = cart.length;
    }

    function openCart() {
        const modal = document.getElementById('cartModal');
        const itemsDiv = document.getElementById('cartItems');
        const totalDiv = document.getElementById('cartTotal');
        const payBtn = document.getElementById('payBtn');

        if (cart.length === 0) {
            itemsDiv.innerHTML = '<p class="empty-cart">Корзина пуста. Добавьте товары из каталога!</p>';
            totalDiv.style.display = 'none';
            payBtn.style.display = 'none';
        } else {
            let html = '<div class="cart-notice">📍 Все заказы забираются <strong>самовывозом</strong> в заведении с 18:00 до его закрытия. Покажите QR-код после оплаты.</div>';
            let total = 0;
            cart.forEach((item, idx) => {
                total += item.price;
                html += `
                    <div class="cart-item">
                        <div class="cart-item-info">
                            <h4>${item.name} <span style="color:#8B0000; font-size:12px;">-${item.discount}%</span></h4>
                            <p>${item.place}</p>
                        </div>
                        <div style="display:flex; align-items:center;">
                            <span class="cart-item-price">${item.price} ₽</span>
                            <button class="cart-item-remove" data-idx="${idx}">✕</button>
                        </div>
                    </div>`;
            });
            itemsDiv.innerHTML = html;
            document.getElementById('totalPrice').textContent = total + ' ₽';
            totalDiv.style.display = 'flex';
            payBtn.style.display = 'block';
            itemsDiv.querySelectorAll('.cart-item-remove').forEach(btn => {
                btn.addEventListener('click', function() { removeFromCart(parseInt(this.dataset.idx)); });
            });
        }
        modal.classList.add('show');
    }

    function removeFromCart(idx) {
        const item = cart[idx];
        cart.splice(idx, 1);
        const btn = document.getElementById(`btn-${item.id}`);
        if (btn) { btn.textContent = 'В корзину'; btn.classList.remove('added'); }
        updateCartCount();
        openCart();
    }

    function closeCart() { document.getElementById('cartModal').classList.remove('show'); }

    function openPayment() {
        closeCart();
        const total = cart.reduce((sum, item) => sum + item.price, 0);
        document.getElementById('payAmount').textContent = total + ' ₽';
        document.getElementById('payTotal').textContent = total + ' ₽';
        document.getElementById('paymentForm').style.display = 'block';
        document.getElementById('paymentSuccess').style.display = 'none';
        document.getElementById('paymentModal').classList.add('show');
    }

    function closePayment() { document.getElementById('paymentModal').classList.remove('show'); }

    function selectPayMethod(el) {
        document.querySelectorAll('.pay-method').forEach(m => m.classList.remove('active'));
        el.classList.add('active');
    }

    function formatCard(input) {
        let value = input.value.replace(/\D/g, '');
        value = value.replace(/(\d{4})(?=\d)/g, '$1 ');
        input.value = value;
    }

    function formatExpiry(input) {
        let value = input.value.replace(/\D/g, '');
        if (value.length >= 2) value = value.substring(0, 2) + '/' + value.substring(2);
        input.value = value;
    }

    function processPayment() {
        document.getElementById('paymentForm').style.display = 'none';
        document.getElementById('paymentSuccess').style.display = 'block';
        document.getElementById('orderNumber').textContent = '#SF-' + Math.floor(Math.random() * 90000 + 10000);
    }

    function clearCart() {
        cart = [];
        updateCartCount();
        document.querySelectorAll('.add-btn').forEach(btn => { btn.textContent = 'В корзину'; btn.classList.remove('added'); });
    }

    function switchTab(tabName) {
        document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
        document.querySelectorAll('nav button').forEach(b => b.classList.remove('active'));
        document.getElementById('tab-' + tabName).classList.add('active');
        const tabNames = ['catalog', 'map', 'how', 'safety', 'support', 'reviews'];
        const idx = tabNames.indexOf(tabName);
        if (idx >= 0) document.querySelectorAll('nav button')[idx].classList.add('active');
        window.scrollTo({ top: 300, behavior: 'smooth' });
    }

    function updateStats() {
        const totalProducts = placesData.reduce((sum, p) => sum + p.products.length, 0);
        document.getElementById('statPlaces').textContent = placesData.length;
        document.getElementById('statProducts').textContent = totalProducts;
    }

    function openPlaceDetail(placeId) {
        const place = placesData.find(p => p.id === placeId);
        if (!place) return;
        document.getElementById('placeDetailImage').style.backgroundImage = `url('${place.image}')`;
        document.getElementById('placeDetailName').textContent = place.name;
        document.getElementById('placeDetailType').textContent = place.typeLabel;
        document.getElementById('placeDetailAddress').textContent = place.address;
        document.getElementById('placeDetailMetro').textContent = place.metro;
        document.getElementById('placeDetailHours').textContent = place.hours;
        document.getElementById('placeDetailRating').textContent = place.rating;
        let productsHTML = '';
        place.products.forEach(prod => {
            productsHTML += `
                <div class="place-detail-product">
                    <div class="place-detail-product-info">
                        <h4>${prod.name}</h4>
                        <div class="pd-ingredients"><span class="ing-icon">🧾</span><span>${prod.ingredients}</span></div>
                        <p class="pd-expiry">⏰ ${prod.expiry}</p>
                    </div>
                    <div class="place-detail-product-prices">
                        <div class="old-price">${prod.oldPrice} ₽</div>
                        <div class="new-price">${prod.newPrice} ₽</div>
                        <div class="discount-badge">-${prod.discount}%</div>
                    </div>
                </div>`;
        });
        document.getElementById('placeDetailProducts').innerHTML = productsHTML;
        document.getElementById('placeDetailModal').classList.add('show');
    }

    function closePlaceDetail() { document.getElementById('placeDetailModal').classList.remove('show'); }

    function addChatMessage(text, isUser) {
        const messagesDiv = document.getElementById('chatMessages');
        const messageDiv = document.createElement('div');
        messageDiv.className = `chat-message ${isUser ? 'user' : 'bot'}`;
        messageDiv.textContent = text;
        messagesDiv.appendChild(messageDiv);
        messagesDiv.scrollTop = messagesDiv.scrollHeight;
    }

    function sendQuickReply(text) {
        addChatMessage(text, true);
        setTimeout(() => {
            addChatMessage(chatResponses[text] || 'Извините, я не понял вопрос. Попробуйте выбрать тему из быстрых ответов или напишите "Связаться с оператором".', false);
        }, 500);
    }

    function sendMessage() {
        const input = document.getElementById('chatInput');
        const text = input.value.trim();
        if (!text) return;
        addChatMessage(text, true);
        input.value = '';
        setTimeout(() => {
            let response = 'Извините, я не понял вопрос. Попробуйте выбрать тему из быстрых ответов или напишите "Связаться с оператором".';
            const lowerText = text.toLowerCase();
            if (lowerText.includes('заказ') || lowerText.includes('купить')) response = chatResponses['Как сделать заказ?'];
            else if (lowerText.includes('скидк') || lowerText.includes('цена')) response = chatResponses['Какие скидки есть?'];
            else if (lowerText.includes('получить') || lowerText.includes('забрать')) response = chatResponses['Как получить заказ?'];
            else if (lowerText.includes('безопасн') || lowerText.includes('качеств')) response = chatResponses['Безопасно ли это?'];
            else if (lowerText.includes('время') || lowerText.includes('работ')) response = chatResponses['Время работы'];
            else if (lowerText.includes('оператор') || lowerText.includes('человек') || lowerText.includes('позвонить')) response = chatResponses['Связаться с оператором'];
            addChatMessage(response, false);
        }, 700);
    }

    function handleChatKeyPress(event) { if (event.key === 'Enter') sendMessage(); }

    function bindEvents() {
        // Переключение вкладок
        document.querySelectorAll('nav button').forEach(btn => btn.addEventListener('click', function() { switchTab(this.dataset.tab); }));
        document.querySelectorAll('[data-nav]').forEach(link => link.addEventListener('click', function(e) { e.preventDefault(); switchTab(this.dataset.nav); }));
        
        // Фильтры и поиск
        document.querySelectorAll('.filter-btn').forEach(btn => btn.addEventListener('click', function() { filterCards(this.dataset.filter, this); }));
        document.getElementById('searchBox').addEventListener('input', function() { searchCards(this.value); });
        
        // Корзина и оплата
        document.getElementById('openCartBtn').addEventListener('click', openCart);
        document.getElementById('closeCartBtn').addEventListener('click', closeCart);
        document.getElementById('payBtn').addEventListener('click', openPayment);
        document.getElementById('closePaymentBtn').addEventListener('click', closePayment);
        document.getElementById('processPaymentBtn').addEventListener('click', processPayment);
        document.getElementById('closeSuccessBtn').addEventListener('click', function() { closePayment(); clearCart(); });
        document.querySelectorAll('.pay-method').forEach(m => m.addEventListener('click', function() { selectPayMethod(this); }));
        document.getElementById('cardNumber').addEventListener('input', function() { formatCard(this); });
        document.getElementById('cardExpiry').addEventListener('input', function() { formatExpiry(this); });
        
        // Карта и детали заведения
        document.querySelectorAll('.map-pin').forEach(pin => pin.addEventListener('click', function() { openPlaceDetail(parseInt(this.dataset.place)); }));
        document.getElementById('closePlaceDetailBtn').addEventListener('click', closePlaceDetail);
        document.getElementById('placeDetailCloseBtn').addEventListener('click', closePlaceDetail);
        
        // Чат поддержки
        document.querySelectorAll('.quick-reply').forEach(btn => btn.addEventListener('click', function() { sendQuickReply(this.dataset.q); }));
        document.getElementById('chatSendBtn').addEventListener('click', sendMessage);
        document.getElementById('chatInput').addEventListener('keypress', handleChatKeyPress);
        
        // Закрытие модалок по клику вне их
        document.querySelectorAll('.modal-overlay').forEach(overlay => {
            overlay.addEventListener('click', function(e) { if (e.target === this) this.classList.remove('show'); });
        });
    }

    document.addEventListener('DOMContentLoaded', function() {
        setCurrentDate();
        renderCards(placesData);
        renderReviews();
        updateStats();
        bindEvents();
    });
</script>
</body>
</html>
