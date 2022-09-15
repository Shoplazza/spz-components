# spz-order-detail

order detail page, handle data from request url, includes tracking/

## Usage

odometer number

`spz-order-detail` must has `template` content
`spz-order-detail` must has `order-id` attributes

```html
<script id="order-locale-json" type="application/json">{
  "order_status": {{ 'i18n.customers.order_status' | t | json }},
  "order_modal": {{ 'i18n.customers.order_modal' | t | json }}
}</script>
<spz-order-detail id="order-detail" order-id="{{ order.order_info.id }}" locale="script:order-locale-json" layout="container">
  <template>
    <div class="order-page page-container">
      <section class="order-header">
        <h3 class="section-heading">{{ 'i18n.customers.orders.order' | t }} #${data.order.order_info.order_no}</h3>
        <ul class="order-brief">
          ${function() {
            const orderInfo = data.order.order_info;

            const statusLangs = {
              opened: {{ 'i18n.customers.order_status.pending' | t | json }},
              placed: {{ 'i18n.customers.order_status.active' | t | json }},
              finished: {{ 'i18n.customers.order_status.completed' | t | json }},
              cancelled: {{ 'i18n.customers.order_status.cancelled' | t | json }},
              post_sale: {{ 'i18n.customers.order_status.post_sale_pending' | t | json }}
            };

            const statusLocale = orderInfo.post_sale_status && orderInfo.post_sale_status !== 'none'
              ? statusLangs.post_sale
              : (statusLangs[orderInfo.status] || orderInfo.status);

            return `
              <li>
                <span class="order-brief--label">{{ 'i18n.customers.orders.order' | t }}</span>
                <span class="order-brief-number">#${orderInfo.order_no}</span>
              </li>
              <li>
                <span class="order-brief--label">{{ 'i18n.customers.orders.date' | t }}</span>
                <span class="order-brief-time">${orderInfo.createTimeFormatted}</span>
              </li>
              <li>
                <span class="order-brief--label">{{ 'i18n.customers.orders.total' | t }}</span>
                <spz-currency layout="container" value="${orderInfo.total}"></spz-currency>
              </li>
              <li>
                <span class="order-brief--label">{{ 'i18n.customers.orders.status' | t }}</span>
                <span class="order-status" data-type="${orderInfo.orderColorStatus}">${statusLocale}</span>
              </li>
            `;
          }()}
        </ul>
      </section>

      {% comment %} order shipment {% endcomment %}
      <section class="order-shipments">
        ${function() {
          if (data.fulfillments.count > 0) {
            return data.fulfillments.fulfillments.map((item, index) => {
              const MONTH_ABBR = [ "Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];

              const createTime = new Date(item.created_at);
              const hours = createTime.getHours();
              const minutes = createTime.getMinutes();
              const meridiem = hours < 12 ? 'am' : 'pm';
              const formatTime = `${createTime.getDate()} ${MONTH_ABBR[createTime.getMonth()]} ${createTime.getFullYear()}, ${hours}:${minutes} ${meridiem}`;

              return `
                <div class="order-shipment">
                  <p class="order-subheading">{{ 'i18n.customers.orders.shipments' | t }}</p>
                  <div class="order-subtitle">{{ 'i18n.customers.orders.package' | t }}&nbsp;#${index + 1}</div>
                  <ul class="order-brief">
                    <li>
                      <span class="order-brief--label">{{ 'i18n.customers.order_details.tracking_number' | t }}</span>
                      <span class="order-brief-number">${item.tracking_number}</span>
                    </li>
                    <li>
                      <span class="order-brief--label">{{ 'i18n.customers.order_details.carrier' | t }}</span>
                      <span>${item.tracking_company}</span>
                    </li>
                    <li>
                      <span class="order-brief--label">{{ 'i18n.customers.order_details.fulfilled' | t }}</span>
                      <span>${formatTime}</span>
                    </li>
                    <li>
                      <span class="order-brief--label">{{ 'i18n.customers.orders.status' | t }}</span>
                      <div class="order-status" data-type="${item.shippingState}">
                        ${data.order.copyWriter['shipStatus'][(data.order.notOrderStatus.includes(item.status) ? 'not_order_' : '') + item.status]}
                      </div>
                    </li>
                  </ul>
                  <div class="order-details">
                    <div class="order-details-head flex justify-between md:hidden">
                      <span class="order-width-300">{{ 'i18n.customers.order_details.product' | t }}</span>
                      <span class="order-width-120">{{ 'i18n.products.product.sku' | t }}</span>
                      <span class="order-width-100">{{ 'i18n.products.product.qty' | t }}</span>
                    </div>

                    ${function() {
                      return item.line_items.map(product => {
                        return `
                          <ul class="order-detail-product">
                            <li class="order-detail-product-intro order-width-300">
                              <a class="order-detail-product-img" href="${product.product_url}">
                                <spz-img
                                  layout="fixed"
                                  width="100"
                                  height="100"
                                  src="${product.image && product.image.src}"
                                  alt="${(product.image && product.image.alt) || product.product_title}"
                                  object-fit="cover"
                                ></spz-img>
                                <span class="order-detail-product-qty lg:hidden">x${product.quantity}</span>
                              </a>
                              <div class="order-detail-product-features flex flex-col">
                                <a class="order-detail-product-title break-words" href="${product.product_url}">${product.product_title}</a>

                                ${function() {
                                  return product.options.map(option => {
                                    return `
                                      <span class="order-detail-product-variant break-words md:hidden">${option.name}&nbsp;:&nbsp;${option.value}</span>
                                    `;
                                  }).join('');
                                }()}

                                <span class="order-detail-product-variant break-words lg:hidden" spz-if="${!!product.optionsLabel}">${product.optionsLabel}</span>
                                <span class="order-detail-product-sku break-words lg:hidden" spz-if="${!!product.sku}">
                                  {{ 'i18n.products.product.sku' | t }}:${product.sku}
                                </span>
                              </div>
                            </li>
                            <li class="order-detail-product-sku break-words order-width-120 md:hidden">${product.sku}</li>
                            <li class="order-detail-product-qty break-words order-width-100 md:hidden">x${product.quantity}</li>
                          </ul>
                        `;
                      }).join('');
                    }()}
                  </div>

                  {%- comment -%} shipment tracking {%- endcomment -%}
                  <div id="tracking-${item.id}" class="hidden order-detail-tracking">
                    <div class="tracking-title">{{ 'i18n.customers.order_details.latest_tracking' | t }}: </div>
                    <spz-render manual layout="container" template="other-tracking-template"></spz-render>
                  </div>

                  <div class="order-actions">
                    ${function() {
                      let actionsHtml = '';

                      if (item.requires_shipping) {
                        actionsHtml += `
                          <button
                            class="button-secondary"
                            id="tracking-btn-${item.id}"
                            role="tracking"
                            tracking-id="${item.tracking_number}"
                            target="tracking-${item.id}"
                            @tap="tracking-${item.id}.toggleClass(class='hidden');tracking-btn-${item.id}.toggleClass(class='tracking');"
                          >
                            <span role="locale-tracking" class="truncate">{{ 'i18n.customers.order_details.tracking' | t }}</span>
                            <span role="locale-fold-tracking" class="hidden truncate">{{ 'i18n.customers.order_details.fold_tracking_info' | t }}</span>
                          </button>
                        `;
                      }

                      if (item.enableTrackingBtn) {
                        actionsHtml += `
                          <button class="button-primary" role="receipt" data-id="${item.id}">
                            {{ 'i18n.customers.order_details.confirm_receipt' | t }}
                          </button>
                        `;
                      }

                      return actionsHtml;
                    }()}
                  </div>
                </div>
              `;
            }).join('');
          }
          return '';
        }()}
      </section>


      {% comment %} fully order information {% endcomment %}
      <section>
        <p class="order-subheading">{{ 'i18n.customers.order_details.order_details' | t }}</p>
        <div class="order-details">
          <div class="order-details-head flex justify-between md:hidden">
            <span class="order-width-300">{{ 'i18n.customers.order_details.product' | t }}</span>
            <span class="order-width-120">{{ 'i18n.products.product.sku' | t }}</span>
            <span class="order-width-100">{{ 'i18n.products.product.qty' | t }}</span>
            <span class="order-width-120">{{ 'i18n.customers.orders.total' | t }}</span>
            <span class="order-width-140">{{ 'i18n.customers.orders.status' | t }}</span>
          </div>

          ${function() {
            return data.order.line_items.map(product => {
              return `
                <ul class="order-detail-product">
                  <li class="order-detail-product-intro order-width-300">
                    <a class="order-detail-product-img" href="${product.product_url}">
                      <spz-img
                        layout="fixed"
                        width="100"
                        height="100"
                        src="${product.image && product.image.src}"
                        alt="${(product.image && product.image.alt) || product.product_title}"
                        object-fit="cover"
                      ></spz-img>
                      <span class="order-detail-product-qty lg:hidden">x${product.quantity}</span>
                    </a>
                    <div class="order-detail-product-features flex flex-col">
                      <span class="order-status break-words" data-type="no-shipping" spz-if="${product.requires_shipping === false}">
                        {{ 'i18n.customers.order_details.no_shipping_required' | t }}
                      </span>
                      <a class="order-detail-product-title break-words" href="${product.product_url}">${product.product_title}</a>

                      ${function() {
                        return product.options.map(option => {
                          return `
                            <span class="order-detail-product-variant break-words md:hidden">${option.name}&nbsp;:&nbsp;${option.value}</span>
                          `;
                        }).join('');
                      }()}

                      <span class="order-detail-product-variant break-words lg:hidden" spz-if="${!!product.optionsLabel}">${product.optionsLabel}</span>
                      <span class="order-detail-product-sku break-words lg:hidden" spz-if="${!!product.sku}">
                        {{ 'i18n.products.product.sku' | t }}:${product.sku}
                      </span>
                      <span class="order-status lg:hidden" data-type="${product.shippingState}">
                        ${data.order.copyWriter['shipStatus'][(data.order.notOrderStatus.includes(product.fulfillment_status) ? 'not_order_' : '') + product.fulfillment_status]}
                      </span>
                    </div>
                  </li>
                  <li class="order-detail-product-sku break-words order-width-120 md:hidden">${product.sku}</li>
                  <li class="order-detail-product-qty break-words order-width-100 md:hidden">x${product.quantity}</li>
                  <li class="order-width-120 break-words md:hidden">
                    <spz-currency layout="container" value="${product.total}"></spz-currency>
                  </li>
                  <li class="order-width-140 break-words md:hidden">
                    <span class="order-status" data-type="${product.shippingState}">
                      ${data.order.copyWriter['shipStatus'][(data.order.notOrderStatus.includes(product.fulfillment_status) ? 'not_order_' : '') + product.fulfillment_status]}
                    </span>
                  </li>
                </ul>
              `;
            }).join('');
          }()}

          <div class="order-detail-summary">
            <section class="order-detail-summary-address">
              <p class="order-detail-summary-subheading">{{ 'i18n.customers.order_details.delivery_address' | t }}</p>
              <div class="order-detail-summary-content flex flex-col">
                <span class="break-words" spz-if="${!!data.order.shipping_address.email}">${data.order.shipping_address.email}</span>
                <span class="break-words" spz-if="${!!data.order.shipping_address.phone}">${data.order.shipping_address.phone}</span>
                <span class="break-words" spz-if="${!!data.order.shipping_address.first_name || !!data.order.shipping_address.last_name}">
                  <span spz-if="${!!data.order.shipping_address.first_name}">${data.order.shipping_address.first_name}&nbsp;</span>
                  <span spz-if="${!!data.order.shipping_address.last_name}">${data.order.shipping_address.last_name}</span>
                </span>
                <span class="break-words" spz-if="${!!data.order.shipping_address.company}">${data.order.shipping_address.company}</span>
                <span class="break-words">${data.order.shipping_address.formattedAddress}</span>
                <span class="break-words" spz-if="${!!data.order.shipping_address.country || !!data.order.shipping_address.zip}">
                  <span spz-if="${!!data.order.shipping_address.country}">${data.order.shipping_address.country}&nbsp;</span>
                  <span spz-if="${!!data.order.shipping_address.zip}">${data.order.shipping_address.zip}</span>
                </span>
              </div>
            </section>
            <section>
              <p class="order-detail-summary-subheading">{{ 'i18n.customers.order_details.payment' | t }}</p>
              <div class="order-detail-summary-content">
                <div class="order-detail-summary-item" spz-if="${!!data.order.order_info.sub_total}">
                  <span>{{ 'i18n.templates.cart.subtotal' | t }}</span>
                  <spz-currency layout="container" value="${data.order.order_info.sub_total}"></spz-currency>
                </div>
                <div class="order-detail-summary-item" spz-if="${!!data.order.order_info.shipping_total}">
                  <span>{{ 'i18n.customers.order_status.shipping' | t }}</span>
                  <spz-currency layout="container" value="${data.order.order_info.shipping_total}"></spz-currency>
                </div>
                <div class="order-detail-summary-item" spz-if="${!!data.order.order_info.tax_total}">
                  <span>{{ 'i18n.customers.order_details.tax' | t }}</span>
                  <spz-currency layout="container" value="${data.order.order_info.tax_total}"></spz-currency>
                </div>
                <div class="order-detail-summary-item" spz-if="${!!data.order.order_info.total_tip_received}">
                  <span>{{ 'i18n.customers.order_details.tips' | t }}</span>
                  <spz-currency layout="container" value="${data.order.order_info.total_tip_received}"></spz-currency>
                </div>
                <div class="order-detail-summary-item" spz-if="${!!data.order.order_info.discount_total}">
                  <span>{{ 'i18n.templates.cart.discount' | t }}</span>
                  <div class="flex">
                    ${data.order.order_info.discount_total > 0 ? '-' : ''}
                    <spz-currency layout="container" value="${data.order.order_info.discount_total}"></spz-currency>
                  </div>
                </div>
                <div class="order-detail-summary-item" spz-if="${!!data.order.order_info.discount_code}">
                  <span>{{ 'i18n.customers.order_details.code' | t }}</span>
                  <div class="order_detail-summary-value">${data.order.order_info.discount_code}</div>
                </div>
                <div class="order-detail-summary-item" spz-if="${!!data.order.order_info.code_discount_total}">
                  <span>{{ 'i18n.customers.order_details.discount_code' | t }}</span>
                  <spz-currency layout="container" value="${data.order.order_info.code_discount_total}"></spz-currency>
                </div>
                <div class="order-detail-summary-item" spz-if="${!!data.order.order_info.total}">
                  <span>{{ 'i18n.customers.orders.total' | t }}</span>
                  <spz-currency layout="container" value="${data.order.order_info.total}"></spz-currency>
                </div>
              </div>
            </section>
          </div>
        </div>

        {%- comment -%} Operation {%- endcomment -%}
        <div class="order-actions" spz-if="${!!data.order.showButtons}">
          ${function() {
            if (!data.order.showButtons) return '';

            let actionsHtml = '';
            if (data.order.enableDeleteOrder) {
              actionsHtml += `
                <button class="button-secondary" data-type="delete_order" role="deleteOrder">
                  {{ 'i18n.customers.order_details.delete_order' | t }}
                </button>
              `;
            }

            if (data.order.enableCancelOrder) {
              actionsHtml += `
                <button class="button-secondary" data-type="cancel" role="cancelOrder">
                  {{ 'i18n.customers.order_status.cancel' | t }}
                </button>
              `;
            }

            if (data.order.enablePayAgain) {
              actionsHtml += `
                <a class="button-primary" data-type="pay_again" role="payAgain" href="/checkout/{{order.order_info.id}}?step=payment_method" target="_blank" data-track="pay_again" data-track-orderId="{{order.order_info.id}}">
                  {{ 'i18n.customers.order_details.pay_again' | t }}
                </a>
              `;
            }

            if (data.order.enablePayNow) {
              actionsHtml += `
                <a class="button-primary" data-type="pay_now" role="payNow" href="/checkout/{{order.order_info.id}}?step=payment_method" target="_blank">
                  {{ 'i18n.customers.order_details.pay_now' | t }}
                </a>
              `;
            }

            if (data.order.enableAddToCartAll) {
              actionsHtml += `
                <button class="relative button-primary" data-type="add_to_cart_all" role="addToCartAll">
                  <span role="content">{{ 'i18n.customers.order_details.add_to_cart' | t }}</span>
                  {% include 'inner_loading', class: 'absolute inset-0' %}
                </button>
              `;
            }

            return actionsHtml;
          }()}
        </div>
      </section>
    </div>
  </template>
</spz-order-detail>
```

#### Layout and style

Support for all layout

## Attributes

### `order-id`

query order id

### `locale`

order locale map
