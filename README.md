import React, { useState } from 'react';
import { Instagram, MapPin, ShoppingCart, Star, Send } from 'lucide-react';
import { Button } from '@/components/ui/button';
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/components/ui/card';
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from '@/components/ui/select';
import { Input } from '@/components/ui/input';
import { Textarea } from '@/components/ui/textarea';

export default function EpiCestTout() {
  const [selectedCategory, setSelectedCategory] = useState('');
  const [selectedProduct, setSelectedProduct] = useState('');
  const [quantity, setQuantity] = useState(1);
  const [customerName, setCustomerName] = useState('');
  const [customerEmail, setCustomerEmail] = useState('');
  const [customerPhone, setCustomerPhone] = useState('');
  const [customerAddress, setCustomerAddress] = useState('');
  const [reviews, setReviews] = useState([
    { id: 1, name: 'Marie L.', rating: 5, comment: 'Service de transport impeccable ! Chauffeur très professionnel.' },
    { id: 2, name: 'Thomas D.', rating: 5, comment: 'Les cookies sont délicieux ! Je recommande à 100%' },
    { id: 3, name: 'Sophie M.', rating: 4, comment: 'Excellents gâteaux apéro pour mes soirées.' }
  ]);
  const [newReview, setNewReview] = useState({ name: '', rating: 5, comment: '' });

  const products = {
    'Transport': [
      'Retour de soirée -20Km',
      'Retour de soirée +20km',
      'Retour de soirée - 80Km max'
    ],
    'Gâteaux Apéro': [
      'Chips',
      'Bretzels',
      'Cacahuètes',
      'Pistaches',
      'Mini pizzas',
      'Curly',
      'Billes de fromage'
    ],
    'Gâteaux': [
      'Gâteau au chocolat',
      'Madeleines',
      'Cookies'
    ],
    'Boissons': [
      'Coca',
      'Fanta',
      'Crazy Tiger',
      'Ice tea',
      'Jus d\'orange',
      'Jus de pomme',
      'Volvic fraise',
      'Pepsi',
      'Sprite',
      'Multifruit',
      'Redbull',
      'Limonade'
    ],
    'Alcools': [
      'Whisky',
      'Rhum',
      'Vodka',
      'Gin',
      'Tequila',
      'Biere'
    ],
    'Bonbons': [
      'Haribo Tagada',
      'Crocodiles',
      'Schtroumpfs',
      'Dragibus',
      'Têtes brûlées',
      'Sucettes',
      'M&M\'s',
      'Maltesers'
    ]
  };

  const handleOrder = () => {
    if (!selectedProduct || !customerName || !customerEmail || !customerPhone || !customerAddress) {
      alert('Veuillez remplir tous les champs obligatoires');
      return;
    }

    const subject = encodeURIComponent('Nouvelle commande EpiC\'est Tout');
    const body = encodeURIComponent(
      `Nouvelle commande:\n\n` +
      `Nom: ${customerName}\n` +
      `Email: ${customerEmail}\n` +
      `Téléphone: ${customerPhone}\n` +
      `Adresse: ${customerAddress}\n` +
      `Catégorie: ${selectedCategory}\n` +
      `Produit: ${selectedProduct}\n` +
      `Quantité: ${quantity}\n\n` +
      `Merci de me contacter pour finaliser la commande.`
    );

    window.location.href = `mailto:Mathis.feurprier@gmail.com?subject=${subject}&body=${body}`;
  };

  const handleAddReview = () => {
    if (!newReview.name || !newReview.comment) {
      alert('Veuillez remplir votre nom et commentaire');
      return;
    }

    setReviews([...reviews, { 
      id: reviews.length + 1, 
      name: newReview.name, 
      rating: newReview.rating, 
      comment: newReview.comment 
    }]);
    
    setNewReview({ name: '', rating: 5, comment: '' });
    alert('Merci pour votre avis !');
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-amber-50 via-orange-50 to-red-50">
      <header className="bg-white shadow-md sticky top-0 z-50">
        <div className="container mx-auto px-4 py-6">
          <div className="flex items-center justify-between">
            <div className="flex items-center gap-4">
              <div className="bg-gradient-to-br from-orange-500 to-red-600 rounded-full p-4 shadow-lg">
                <div className="text-white font-bold text-xl">Epi</div>
              </div>
              <div>
                <h1 className="text-3xl font-bold bg-gradient-to-r from-orange-600 to-red-600 bg-clip-text text-transparent">
                  EpiC'est Tout
                </h1>
                <p className="text-sm text-muted-foreground">Votre partenaire soirée & gourmandise</p>
              </div>
            </div>
            
            <div className="flex gap-4">
              <a 
                href="https://www.instagram.com/epicesttout72?igsh=dXJmeHZ2eGFnNHhi&utm_source=qr" 
                target="_blank" 
                rel="noopener noreferrer"
                className="bg-gradient-to-br from-purple-500 to-pink-500 p-3 rounded-full hover:scale-110 transition-transform shadow-lg"
              >
                <Instagram className="w-6 h-6 text-white" />
              </a>
              <a 
                href="https://snapchat.com/t/hHZtsJER" 
                target="_blank" 
                rel="noopener noreferrer"
                className="bg-gradient-to-br from-yellow-400 to-yellow-500 p-3 rounded-full hover:scale-110 transition-transform shadow-lg"
              >
                <svg className="w-6 h-6 text-white" viewBox="0 0 24 24" fill="currentColor">
                  <path d="M12.206.793c.99 0 4.347.276 5.93 3.821.529 1.193.403 3.219.299 4.847l-.003.06c-.012.18-.022.345-.03.51.075.045.203.09.401.09.3-.016.659-.12 1.033-.301.165-.088.344-.104.464-.104.182 0 .359.029.509.09.45.149.734.479.734.838.015.449-.39.839-1.213 1.168-.089.029-.209.075-.344.119-.45.135-1.139.36-1.333.81-.09.224-.061.524.12.868l.015.015c.06.136 1.526 3.475 4.791 4.014.255.044.435.27.42.509 0 .075-.015.149-.045.225-.24.569-1.273.988-3.146 1.271-.059.091-.12.375-.164.57-.029.179-.074.36-.134.553-.076.271-.27.405-.555.405h-.03c-.135 0-.313-.031-.538-.074-.36-.075-.765-.135-1.273-.135-.3 0-.599.015-.913.074-.6.104-1.123.464-1.723.884-.853.599-1.826 1.288-3.294 1.288-.06 0-.119-.015-.18-.015h-.149c-1.468 0-2.427-.675-3.279-1.288-.599-.42-1.107-.779-1.707-.884-.314-.045-.629-.074-.928-.074-.54 0-.958.089-1.272.149-.211.043-.391.074-.54.074-.374 0-.523-.224-.583-.42-.061-.192-.09-.389-.135-.567-.046-.181-.105-.494-.166-.57-1.918-.222-2.95-.642-3.189-1.226-.031-.063-.052-.12-.061-.18-.015-.255.165-.494.42-.554 3.264-.54 4.73-3.879 4.791-4.02l.016-.029c.18-.345.224-.645.119-.869-.195-.434-.884-.658-1.332-.809-.121-.029-.24-.074-.346-.119-1.107-.435-1.257-.93-1.197-1.273.09-.479.674-.793 1.168-.793.146 0 .27.029.383.074.42.194.789.3 1.104.3.234 0 .384-.06.465-.105l-.046-.569c-.098-1.626-.225-3.651.307-4.837C7.392 1.077 10.739.807 11.727.807l.419-.015h.06z"/>
                </svg>
              </a>
            </div>
          </div>
        </div>
      </header>

      <section className="container mx-auto px-4 py-12">
        <div className="text-center mb-12">
          <h2 className="text-5xl font-bold mb-4 bg-gradient-to-r from-orange-600 to-red-600 bg-clip-text text-transparent">
            Bienvenue chez EpiC'est Tout !
          </h2>
          <p className="text-xl text-foreground max-w-2xl mx-auto">
            Votre service tout-en-un pour des soirées réussies : transport sécurisé et délices gourmands
          </p>
        </div>

        <div className="grid md:grid-cols-2 gap-8 mb-16">
          <Card className="border-2 border-orange-200 hover:shadow-xl transition-shadow">
            <CardHeader className="bg-gradient-to-br from-orange-100 to-red-100">
              <div className="flex items-center gap-3">
                <MapPin className="w-8 h-8 text-orange-600" />
                <CardTitle className="text-2xl">Transport Nocturne</CardTitle>
              </div>
              <CardDescription className="text-base">Rentrez en toute sécurité après vos soirées</CardDescription>
            </CardHeader>
            <CardContent className="pt-6">
              <ul className="space-y-3">
                <li className="flex items-start gap-2">
                  <Star className="w-5 h-5 text-orange-500 mt-1 flex-shrink-0" />
                  <span>Chauffeurs expérimentés et professionnels</span>
                </li>
                <li className="flex items-start gap-2">
                  <Star className="w-5 h-5 text-orange-500 mt-1 flex-shrink-0" />
                  <span>Service disponible de 23h à 7h</span>
                </li>
                <li className="flex items-start gap-2">
                  <Star className="w-5 h-5 text-orange-500 mt-1 flex-shrink-0" />
                  <span>Tarifs calculer avec l'appli Mappy</span>
                </li>
              </ul>
            </CardContent>
          </Card>

          <Card className="border-2 border-orange-200 hover:shadow-xl transition-shadow">
            <CardHeader className="bg-gradient-to-br from-amber-100 to-orange-100">
              <div className="flex items-center gap-3">
                <ShoppingCart className="w-8 h-8 text-orange-600" />
                <CardTitle className="text-2xl">Produits Gourmands</CardTitle>
              </div>
              <CardDescription className="text-base">Des délices pour toutes vos envies</CardDescription>
            </CardHeader>
            <CardContent className="pt-6">
              <ul className="space-y-3">
                <li className="flex items-start gap-2">
                  <Star className="w-5 h-5 text-orange-500 mt-1 flex-shrink-0" />
                  <span>Gâteaux apéro</span>
                </li>
                <li className="flex items-start gap-2">
                  <Star className="w-5 h-5 text-orange-500 mt-1 flex-shrink-0" />
                  <span>Cookies et d'autres gateaux</span>
                </li>
                <li className="flex items-start gap-2">
                  <Star className="w-5 h-5 text-orange-500 mt-1 flex-shrink-0" />
                  <span>Boissons et sélection d'alcools</span>
                </li>
              </ul>
            </CardContent>
          </Card>
        </div>

        <Card className="mb-16 border-2 border-orange-300 shadow-2xl">
          <CardHeader className="bg-gradient-to-r from-orange-500 to-red-500 text-white">
            <CardTitle className="text-3xl text-center">Passez votre commande</CardTitle>
            <CardDescription className="text-orange-50 text-center text-base">
              Sélectionnez vos produits et nous vous contacterons rapidement
            </CardDescription>
          </CardHeader>
          <CardContent className="pt-8 space-y-6">
            <div className="grid md:grid-cols-2 gap-6">
              <div>
                <label className="block text-sm font-medium mb-2 text-foreground">Votre nom *</label>
                <Input 
                  placeholder="Votre nom complet" 
                  value={customerName}
                  onChange={(e) => setCustomerName(e.target.value)}
                  className="border-orange-200"
                />
              </div>
              
              <div>
                <label className="block text-sm font-medium mb-2 text-foreground">Votre email *</label>
                <Input 
                  type="email"
                  placeholder="votre@email.com" 
                  value={customerEmail}
                  onChange={(e) => setCustomerEmail(e.target.value)}
                  className="border-orange-200"
                />
              </div>
            </div>

            <div className="grid md:grid-cols-2 gap-6">
              <div>
                <label className="block text-sm font-medium mb-2 text-foreground">Numéro de téléphone *</label>
                <Input 
                  type="tel"
                  placeholder="06 12 34 56 78" 
                  value={customerPhone}
                  onChange={(e) => setCustomerPhone(e.target.value)}
                  className="border-orange-200"
                />
              </div>

              <div>
                <label className="block text-sm font-medium mb-2 text-foreground">Adresse *</label>
                <Input 
                  placeholder="Votre adresse complète" 
                  value={customerAddress}
                  onChange={(e) => setCustomerAddress(e.target.value)}
                  className="border-orange-200"
                />
              </div>
            </div>

            <div>
              <label className="block text-sm font-medium mb-2 text-foreground">Catégorie *</label>
              <Select onValueChange={(value) => {
                setSelectedCategory(value);
                setSelectedProduct('');
              }}>
                <SelectTrigger className="border-orange-200">
                  <SelectValue placeholder="Choisissez une catégorie" />
                </SelectTrigger>
                <SelectContent>
                  <SelectItem value="Transport">🚗 Transport Nocturne</SelectItem>
                  <SelectItem value="Gâteaux Apéro">🥐 Gâteaux Apéro</SelectItem>
                  <SelectItem value="Gâteaux">🍪 Gâteaux</SelectItem>
                  <SelectItem value="Boissons">🥤 Boissons</SelectItem>
                  <SelectItem value="Alcools">🍷 Alcools</SelectItem>
                  <SelectItem value="Bonbons">🍬 Bonbons</SelectItem>
                </SelectContent>
              </Select>
            </div>

            {selectedCategory && (
              <div>
                <label className="block text-sm font-medium mb-2 text-foreground">Produit *</label>
                <Select onValueChange={setSelectedProduct}>
                  <SelectTrigger className="border-orange-200">
                    <SelectValue placeholder="Sélectionnez un produit" />
                  </SelectTrigger>
                  <SelectContent>
                    {products[selectedCategory as keyof typeof products]?.map((product) => (
                      <SelectItem key={product} value={product}>
                        {product}
                      </SelectItem>
                    ))}
                  </SelectContent>
                </Select>
              </div>
            )}

            {selectedProduct && (
              <div>
                <label className="block text-sm font-medium mb-2 text-foreground">Quantité</label>
                <Input 
                  type="number" 
                  min="1" 
                  value={quantity}
                  onChange={(e) => setQuantity(parseInt(e.target.value) || 1)}
                  className="border-orange-200"
                />
              </div>
            )}

            <Button 
              onClick={handleOrder}
              className="w-full bg-gradient-to-r from-orange-500 to-red-600 hover:from-orange-600 hover:to-red-700 text-white text-lg py-6 shadow-lg"
            >
              <Send className="w-5 h-5 mr-2" />
              Commander maintenant
            </Button>
          </CardContent>
        </Card>

        <div className="grid md:grid-cols-2 gap-8 mb-16">
          <Card className="border-2 border-orange-200">
            <CardHeader className="bg-gradient-to-br from-amber-100 to-orange-100">
              <CardTitle className="text-2xl">Avis clients</CardTitle>
              <CardDescription>Ce que nos clients disent de nous</CardDescription>
            </CardHeader>
            <CardContent className="pt-6">
              <div className="space-y-4 max-h-96 overflow-y-auto">
                {reviews.map((review) => (
                  <div key={review.id} className="bg-white p-4 rounded-lg border border-orange-100">
                    <div className="flex items-center justify-between mb-2">
                      <span className="font-semibold text-foreground">{review.name}</span>
                      <div className="flex gap-1">
                        {[...Array(review.rating)].map((_, i) => (
                          <Star key={i} className="w-4 h-4 fill-orange-400 text-orange-400" />
                        ))}
                      </div>
                    </div>
                    <p className="text-sm text-muted-foreground">{review.comment}</p>
                  </div>
                ))}
              </div>
            </CardContent>
          </Card>

          <Card className="border-2 border-orange-200">
            <CardHeader className="bg-gradient-to-br from-orange-100 to-red-100">
              <CardTitle className="text-2xl">Laissez un avis</CardTitle>
              <CardDescription>Partagez votre expérience avec nous</CardDescription>
            </CardHeader>
            <CardContent className="pt-6 space-y-4">
              <div>
                <label className="block text-sm font-medium mb-2 text-foreground">Votre nom</label>
                <Input 
                  placeholder="Votre nom" 
                  value={newReview.name}
                  onChange={(e) => setNewReview({...newReview, name: e.target.value})}
                  className="border-orange-200"
                />
              </div>

              <div>
                <label className="block text-sm font-medium mb-2 text-foreground">Note</label>
                <Select 
                  value={newReview.rating.toString()}
                  onValueChange={(value) => setNewReview({...newReview, rating: parseInt(value)})}
                >
                  <SelectTrigger className="border-orange-200">
                    <SelectValue />
                  </SelectTrigger>
                  <SelectContent>
                    <SelectItem value="5">⭐⭐⭐⭐⭐ Excellent</SelectItem>
                    <SelectItem value="4">⭐⭐⭐⭐ Très bien</SelectItem>
                    <SelectItem value="3">⭐⭐⭐ Bien</SelectItem>
                    <SelectItem value="2">⭐⭐ Moyen</SelectItem>
                    <SelectItem value="1">⭐ Décevant</SelectItem>
                  </SelectContent>
                </Select>
              </div>

              <div>
                <label className="block text-sm font-medium mb-2 text-foreground">Votre commentaire</label>
                <Textarea 
                  placeholder="Partagez votre expérience..." 
                  value={newReview.comment}
                  onChange={(e) => setNewReview({...newReview, comment: e.target.value})}
                  className="border-orange-200 min-h-24"
                />
              </div>

              <Button 
                onClick={handleAddReview}
                className="w-full bg-gradient-to-r from-orange-500 to-red-600 hover:from-orange-600 hover:to-red-700"
              >
                Publier mon avis
              </Button>
            </CardContent>
          </Card>
        </div>
      </section>

      <footer className="bg-gradient-to-r from-orange-600 to-red-600 text-white py-8 mt-16">
        <div className="container mx-auto px-4 text-center">
          <div className="mb-4">
            <h3 className="text-2xl font-bold mb-2">EpiC'est Tout</h3>
            <p className="text-orange-100">Votre partenaire soirée & gourmandise</p>
          </div>
          
          <div className="flex justify-center gap-6 mb-4">
            <a 
              href="https://www.instagram.com/epicesttout72?igsh=dXJmeHZ2eGFnNHhi&utm_source=qr" 
              target="_blank" 
              rel="noopener noreferrer"
              className="hover:text-orange-200 transition-colors"
            >
              <Instagram className="w-6 h-6" />
            </a>
            <a 
              href="https://snapchat.com/t/hHZtsJER" 
              target="_blank" 
              rel="noopener noreferrer"
              className="hover:text-orange-200 transition-colors"
            >
              <svg className="w-6 h-6" viewBox="0 0 24 24" fill="currentColor">
                <path d="M12.206.793c.99 0 4.347.276 5.93 3.821.529 1.193.403 3.219.299 4.847l-.003.06c-.012.18-.022.345-.03.51.075.045.203.09.401.09.3-.016.659-.12 1.033-.301.165-.088.344-.104.464-.104.182 0 .359.029.509.09.45.149.734.479.734.838.015.449-.39.839-1.213 1.168-.089.029-.209.075-.344.119-.45.135-1.139.36-1.333.81-.09.224-.061.524.12.868l.015.015c.06.136 1.526 3.475 4.791 4.014.255.044.435.27.42.509 0 .075-.015.149-.045.225-.24.569-1.273.988-3.146 1.271-.059.091-.12.375-.164.57-.029.179-.074.36-.134.553-.076.271-.27.405-.555.405h-.03c-.135 0-.313-.031-.538-.074-.36-.075-.765-.135-1.273-.135-.3 0-.599.015-.913.074-.6.104-1.123.464-1.723.884-.853.599-1.826 1.288-3.294 1.288-.06 0-.119-.015-.18-.015h-.149c-1.468 0-2.427-.675-3.279-1.288-.599-.42-1.107-.779-1.707-.884-.314-.045-.629-.074-.928-.074-.54 0-.958.089-1.272.149-.211.043-.391.074-.54.074-.374 0-.523-.224-.583-.42-.061-.192-.09-.389-.135-.567-.046-.181-.105-.494-.166-.57-1.918-.222-2.95-.642-3.189-1.226-.031-.063-.052-.12-.061-.18-.015-.255.165-.494.42-.554 3.264-.54 4.73-3.879 4.791-4.02l.016-.029c.18-.345.224-.645.119-.869-.195-.434-.884-.658-1.332-.809-.121-.029-.24-.074-.346-.119-1.107-.435-1.257-.93-1.197-1.273.09-.479.674-.793 1.168-.793.146 0 .27.029.383.074.42.194.789.3 1.104.3.234 0 .384-.06.465-.105l-.046-.569c-.098-1.626-.225-3.651.307-4.837C7.392 1.077 10.739.807 11.727.807l.419-.015h.06z"/>
              </svg>
            </a>
          </div>

          <div className="mb-6 border-t border-orange-400 pt-6">
            <h4 className="text-xl font-bold mb-4">Horaires</h4>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-2 max-w-2xl mx-auto text-orange-100">
              <div className="flex justify-between px-4">
                <span className="font-medium">Lundi</span>
                <span>22h - 1h</span>
              </div>
              <div className="flex justify-between px-4">
                <span className="font-medium">Mardi</span>
                <span>22h - 1h</span>
              </div>
              <div className="flex justify-between px-4">
                <span className="font-medium">Mercredi</span>
                <span>22h - 1h</span>
              </div>
              <div className="flex justify-between px-4">
                <span className="font-medium">Jeudi</span>
                <span>22h - 1h</span>
              </div>
              <div className="flex justify-between px-4">
                <span className="font-medium">Vendredi</span>
                <span>22h - 7h</span>
              </div>
              <div className="flex justify-between px-4">
                <span className="font-medium">Samedi</span>
                <span>20h - 7h</span>
              </div>
            </div>
          </div>
          
          <p className="text-sm text-orange-100">
            © 2024 EpiC'est Tout. Tous droits réservés.
          </p>
        </div>
      </footer>
    </div>
  );
}
